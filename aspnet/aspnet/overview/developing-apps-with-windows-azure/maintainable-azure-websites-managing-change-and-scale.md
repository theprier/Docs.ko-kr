---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: '실습 랩: Azure 웹 사이트를 유지 관리 가능한: 변경 및 크기 조정 관리 | Microsoft Docs'
author: rick-anderson
description: 이 랩에서 Microsoft Azure 손쉽게 방법을를 빌드 및 프로덕션 환경에 웹 사이트 배포에 대해 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: a79921681b4e742b5cd23f7119d19f4dd74c3f83
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>실습 랩: Azure 웹 사이트를 유지 관리 가능한: 변경 및 크기 조정 관리
====================
으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](http://aka.ms/webcamps-training-kit)

> Microsoft Azure를 사용 하면 쉽게 만들고 프로덕션 환경에 웹 사이트를 배포 합니다. 하지만 응용 프로그램은 라이브 때 완료 되지 않았습니다, 그리고 방금 시작! 변경 요구 사항, 데이터베이스 업데이트, 배율 등을 처리 해야 합니다. 다행히 Azure 앱 서비스에는 다량의 원활 하 게 실행 하 여 사이트를 유지 하는 데 유용한 기능을 거둘 수 있습니다.
> 
> Azure는 안전 하 고 유연한 개발, 배포 및 확장 크기는 웹 응용 프로그램에 대 한 옵션을 제공 합니다. 만들기 및 배포 인프라를 관리할 필요 없이 응용 프로그램에 기존 도구를 활용 합니다.
> 
> 프로 비전 프로덕션 웹 응용 프로그램 사용자가 직접 분에서 쉽게 즐겨 찾는 개발 도구를 사용 하 여 만든 콘텐츠를 배포 하 여 합니다. 기존 사이트를 지 원하는 소스 제어에서 직접 배포할 수 있습니다 **Git**, **GitHub**, **Bitbucket**, **TFS**, 및에  **DropBox**합니다. 즐겨 찾는 IDE에서 직접 또는 스크립트를 사용 하 여 배포 **PowerShell** windows에서 또는 **CLI** 모든 OS에서 실행 되는 도구입니다. 배포 된 후에 사이트를 연속 배포를 지 원하는 지속적으로 최신 상태로 유지 합니다.
> 
> Azure 큰 또는 작은 모든 데이터에 대 한 내구성이 있는 확장 가능한 클라우드 저장소, 백업 및 복구 솔루션 제공합니다. 응용 프로그램을 프로덕션 환경, 테이블, Blob 및 SQL 데이터베이스와 같은 저장소 서비스를 배포할 때는 클라우드에서 응용 프로그램을 확장 하는 데 도움이.
> 
> SQL 데이터베이스와 새 버전의 응용 프로그램을 배포 하는 경우 생산성 데이터베이스를 최신 상태로 유지 해야 합니다. 에 감사 드립니다 **Entity Framework Code First 마이그레이션을**, 개발 및 배포 데이터 모델의 분에서 환경을 업데이트할 간소화 되었습니다. 이 실습 랩에서 Microsoft Azure에서 프로덕션 환경에 웹 앱을 배포할 때 발생할 수 있습니다 다른 항목에 표시 됩니다.
> 
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.
> 
> 이 항목의 깊이 있는 자세한 검사에 대 한 참조는 [Azure 전자책으로 실제 클라우드 응용 프로그램 빌딩](building-real-world-cloud-apps-with-windows-azure/introduction.md)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- 기존 모델과 함께 엔터티 프레임 워크 마이그레이션을 사용 하도록 설정
- 개체 모델 및 그에 따라 엔터티 프레임 워크 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.
- Git를 사용 하 여 Azure 응용 프로그램 서비스에 배포
- Azure 관리 포털을 사용 하 여 이전 배포 rollback
- Azure 저장소를 사용 하 여 웹 앱의 크기를 조정 하려면
- Azure 관리 포털을 사용 하 여 웹 응용 프로그램에 대 한 자동 크기 조정 구성
- 만들기 및 Visual Studio에서 부하 테스트 프로젝트 구성

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음은이 실습 랩을 완료 하려면 필요 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상
- [Azure SDK for.NET 2.2](https://www.microsoft.com/windowsazure/sdk/)
- [GIT 버전 제어 시스템입니다.](http://git-scm.com/download)
- Microsoft Azure 구독 

    - 에 등록 한 [무료 평가판](http://aka.ms/watk-freetrial)
    - 인 경우 Visual Studio Professional, Test Professional, Premium 또는 Ultimate MSDN 또는 MSDN 플랫폼 구독자와 활성화 프로그램 [MSDN 혜택](http://aka.ms/watk-msdn) Azure에서 개발 및 테스트를 시작 하려면 지금
    - [BizSpark](http://aka.ms/watk-bizspark) 멤버는 자동으로 Azure 수신 통해 자신의 Visual Studio Ultimate with MSDN 구독 혜택
    - 멤버는 [Microsoft 파트너 네트워크](http://aka.ms/watk-mpn) Cloud Essentials 프로그램 수신 비용 없이 월간 Azure 크레딧

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기를 열고에 랩 찾아보기 **소스** 폴더입니다.
2. 마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택 **관리자 권한으로 실행** 환경을 구성 되며이 랩에 대 한 Visual Studio 코드 조각을 설치 하는 설치 프로세스를 시작 합니다.
3. 사용자 계정 컨트롤 대화 상자가 표시 하 고, 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각을 사용 하 여

랩 문서를 통해 코드 블록을 삽입 하도록 합니다. 사용자 편의 위해이 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

> [!NOTE]
> 각 연습에는 시작 솔루션 동반 되는 **시작** 개별적으로 각 연습에 따라 할 수 있는 작업의 폴더입니다. 주의 하십시오 연습 하는 동안 추가 된 코드 조각은 솔루션 시작이 항목에서 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다. 실행에 대 한 소스 코드에서 찾아볼 수 있습니다는 **끝** 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션에 포함 된 폴더입니다. 이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [Entity Framework 마이그레이션을 사용 하 여](#Exercise1)
2. [스테이징 웹 응용 프로그램 배포](#Exercise2)
3. [프로덕션 환경에서 배포 Rollback을 수행합니다.](#Exercise3)
4. [Azure 저장소를 사용 하 여 배율을](#Exercise4)
5. [웹 앱에 대 한 자동 크기 조정을 사용할](#Exercise5) (Visual Studio 2013 Ultimate edition에 대 한 선택 사항)

예상 소요 시간: **75 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>연습 1: Entity Framework 마이그레이션을 사용 하 여

응용 프로그램을 개발 하는 데이터 모델에는 시간이 지남에 따라 변경 될 수 있습니다. (새 버전을 만드는) 하는 경우 이러한 변경 내용은 기존 모델 데이터베이스에 영향을 줄 수 및 데이터베이스를 오류를 방지 하려면 최신 상태로 유지 해야 합니다.

사용자의 모델에 이러한 변경의 추적을 간소화 하기 위해 **Entity Framework Code First 마이그레이션을** 자동으로 데이터베이스 스키마를 사용 하 여 모델을 비교 하는 변경 내용을 검색 하 고 데이터베이스를 업데이트 하는 특정 코드를 생성 합니다. 새로 만들기 *버전* 데이터베이스입니다.

이 연습을 사용 하도록 설정 하는 방법을 보여 줍니다. **마이그레이션** 응용 프로그램을 쉽게 검색 하는 방법을 사용자 데이터베이스를 업데이트 하도록 변경 합니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>작업 1-사용 하도록 설정 마이그레이션

사용 하도록 설정 하는 단계를 진행 합니다이 태스크에서는 **Entity Framework Code First 마이그레이션을** 에 **들은 퀴즈** 데이터베이스, 모델을 변경 하 고에서 이러한 변경 내용이 반영 하는 방법을 이해는 데이터베이스입니다.

1. Visual Studio를 열고 열기는 **GeekQuiz.sln** 에서 솔루션 파일 **Source\Ex1 UsingEntityFrameworkMigrations\Begin**합니다.
2. 다운로드 및 설치 하기 위해 솔루션을 빌드하는 **NuGet** 패키지 종속 합니다. 이렇게 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **솔루션 빌드** 하거나 키를 눌러 **Ctrl + Shift + B**합니다.
3. **도구** 선택 Visual Studio에서 메뉴 **라이브러리 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다.
4. 에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다. 기존 모델을 기반으로 하는 초기 마이그레이션 생성 됩니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![마이그레이션을 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "마이그레이션을 사용 하도록 설정")

    *마이그레이션을 사용 하도록 설정*

    > [!NOTE]
    > 이 명령은 추가 **마이그레이션** 파일을 포함 하 게 퀴즈 프로젝트에이 폴더의 이름은 **Configuration.cs**합니다. **구성** 클래스를 사용 하 여 컨텍스트에 대 한 마이그레이션 작동 하는 방법을 구성할 수 있습니다.
5. 마이그레이션을 사용 하도록 설정, 업데이트 해야는 **구성** 초기 데이터에 데이터베이스를 채우는 클래스는 **들은 퀴즈** 필요 합니다. 아래 **마이그레이션**, 대체는 **Configuration.cs** 와 파일에 있는 **Source\Assets** 이 랩의 폴더입니다.

    > [!NOTE]
    > 이후 **마이그레이션** 호출 됩니다는 **시드** 레코드가 데이터베이스에 중복 되지 있는지 확인 해야 하는 모든 데이터베이스 업데이트 메서드를 합니다. **AddOrUpdate** 방법은 중복 데이터 방지 하는 데 도움이 됩니다.
6. 초기 마이그레이션을 추가 하려면 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.

    > [!NOTE]
    > 명명 된 데이터베이스가 없습니다. 인지 확인 &quot;GeekQuizProd&quot; 여 LocalDB 인스턴스에서 합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![기본 스키마 마이그레이션 추가](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "추가 기본 스키마 마이그레이션")

    *기본 스키마 마이그레이션 추가*

    > [!NOTE]
    > **추가 마이그레이션** 마지막 마이그레이션 만들어진 후 모델에 대 한 변경 내용에 따라 다음 마이그레이션을 스 캐 폴드 됩니다. 이 경우 프로젝트의 첫 번째 마이그레이션 이기에 정의 된 모든 테이블을 만드는 스크립트를 추가 되는 **TriviaContext** 클래스입니다.
7. 다음 명령을 실행 하 여 데이터베이스를 업데이트 하려면 마이그레이션을 실행 합니다. 이 명령에 지정 합니다는 **Verbose** 플래그 대상 데이터베이스에 적용 중인 SQL 문을 볼 수 있습니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![초기 데이터베이스 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "초기 데이터베이스 만들기")

    *초기 데이터베이스를 만드는 중*

    > [!NOTE]
    > **데이터베이스 업데이트** 보류 중인 마이그레이션을 데이터베이스에 적용 됩니다. 이 경우 web.config 파일에 정의 된 연결 문자열을 사용 하 여 데이터베이스를 만들어집니다.
8. 로 이동 **보기** 메뉴를 열고 다음 **SQL Server 개체 탐색기**합니다.

    ![SQL Server 개체 탐색기에서 열기](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server 개체 탐색기에서 열기")

    *SQL Server 개체 탐색기에서 열기*
9. 에 **SQL Server 개체 탐색기** 창에서 마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스를 연결할는 **SQL Server** 노드를 선택 하 고 **SQL Server 추가...**  옵션입니다.

    ![SQL Server 인스턴스를 추가](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server 인스턴스를 추가 합니다.")

    *SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*
10. 설정의 **서버 이름** 를 *(localdb) \v11.0* 둡니다 **Windows 인증** 인증 모드로 합니다. 클릭 **연결** 를 계속 합니다.

    ![LocalDB에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB에 연결")

    *LocalDB에 연결*
11. 열기는 **GeekQuizProd** 데이터베이스를 확장 하 고는 **테이블** 노드. 볼 수 있듯이 **Update-database** 명령이 생성에 정의 된 모든 테이블의 **TriviaContext** 클래스입니다. 찾기의 **dbo입니다. TriviaQuestions** 테이블 및 열 노드를 엽니다. 다음 태스크에서는이 테이블에 새 열 추가 사용 하 여 데이터베이스를 업데이트 **마이그레이션**합니다.

    ![Trivia 질문 열](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia 질문 열")

    *Trivia 질문 열*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>작업 2-마이그레이션을 사용 하 여 데이터베이스 스키마를 업데이트

이 작업을 사용 하 여 **Entity Framework Code First 마이그레이션을** 하 모델 변경 사항을 검색 하 고 데이터베이스를 업데이트 하는 데 필요한 코드를 생성 합니다. 업데이트 하는 **TriviaQuestions** 새 속성을 추가 하 여 엔터티. 다음 테이블에 새 열을 포함 하는 새 마이그레이션 만들려면 명령을 실행 합니다.

1. **솔루션 탐색기**, 두 번 클릭는 **TriviaQuestion.cs** 내에 있는 파일의 **모델** 폴더입니다.
2. 라는 새 속성이 추가 **힌트**다음 코드 조각에서와 같이 합니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. 에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다. 새 마이그레이션 부문의 변경을 반영 생성 됩니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![추가 마이그레이션](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "추가 마이그레이션")

    *추가 마이그레이션*

    > [!NOTE]
    > 두 가지 방법으로 구성 된 마이그레이션 파일 **를** 및 **아래로**합니다.
    > 
    > - **를** 메서드를 사용 하 여 현재 버전의 응용 프로그램 해야 데이터베이스에 적용할 변경 내용을 지정할 수는 있습니다.
    > - **아래로** 에 추가한 변경 내용이 되돌리는 것 하는 데 사용 되는 **를** 메서드.
    > 
    > 타임 스탬프 순서 및 마지막 업데이트 이후 사용 되지 않은 하는 항목만에서 모든 마이그레이션 데이터베이스 마이그레이션 데이터베이스를 업데이트할 때 실행 됩니다 (의 \_적용 된 마이그레이션이 어떤 MigrationHistory 테이블의 추적). **를** 모든 마이그레이션의 메서드는 호출 되 고 데이터베이스에 앞서 지정한 같이 변경 됩니다. 이전 마이그레이션이으로 다시 돌아가십시오 계속 사용 하려면 우리는 **아래로** 메서드를 호출 하 여 반대 순서로 변경 내용을 다시 실행 하는 합니다.
4. 에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. 출력은 **Update-database** 생성 된 명령을 **Alter Table** SQL 문이 새 열을 추가 하는 **TriviaQuestions** 아래 이미지에 나와 있는 것 처럼 테이블입니다.

    ![열의 SQL 문을 생성 추가](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "열 SQL 문을 생성 된 추가")

    *추가 열 SQL 문 생성*
6. **SQL Server 개체 탐색기**, 새로 고침의 **dbo입니다. TriviaQuestions** 테이블을 확인 하는 새 **힌트** 열이 표시 됩니다.

    ![새 힌트 열을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "새 힌트 열 표시")

    *새 힌트 열 표시*
7. 에 **TriviaQuestion.cs** 편집기를 추가 **StringLength** 제약 조건에는 *힌트* 속성을 다음 코드 조각에 나와 있는 것 처럼 합니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. 에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. 에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. 출력은 **Update-database** 생성 된 명령을 **Alter Table** SQL 문을 업데이트 하는 *힌트* 열 유형의 **TriviaQuestions** 아래 이미지에 나와 있는 것 처럼 테이블입니다.

    ![Alter column SQL 문에서 생성 된](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 문에서 생성")

    *Alter column SQL 문에서 생성*
11. **SQL Server 개체 탐색기**, 새로 고침의 **dbo입니다. TriviaQuestions** 테이블을 확인 하 고 **힌트** 열 형식이 **nvarchar(150)**합니다.

    ![새 제약 조건을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "새 제약 조건을 보여 주는")

    *새 제약 조건을 보여 주는*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>스테이징 웹 앱을 배포 하는 연습 2:

**Azure 앱 서비스에서 앱을 웹** 준비 된 게시를 수행할 수 있습니다. 준비 된 게시의 각 기본 프로덕션 사이트에 대 한 준비 사이트 슬롯을 만들고 작동 중단 시간 없이 이러한 슬롯을 전환할 수 있습니다. 공개적으로 해제 하기 전에 변경 내용 유효성 검사, 점차 사이트 콘텐츠를 통합 하 고 변경 내용을 정상적으로 작업할 경우 롤백될에 매우 유용 합니다.

이 연습에서는 배포는 **들은 퀴즈** Git 소스 제어를 사용 하 여 웹 응용 프로그램의 스테이징 환경에 응용 프로그램입니다. 이렇게 하려면 웹 앱 만들기 및 관리 포털에서 필수 구성 요소를 프로 비전를 하는 구성 된 **Git** 리포지토리 및 응용 프로그램을 푸시 하도록 소스 코드를 로컬 컴퓨터에서 스테이징 슬롯입니다. 또한와 프로덕션 데이터베이스를 업데이트 합니다는 **Code First 마이그레이션을** 이전 연습에서 만든 합니다. 그런 다음 해당 작업을 확인 하려면이 테스트 환경에서 응용 프로그램을 실행 합니다. 했으면 한다는 예상에 따라 작동, 프로덕션 환경에 응용 프로그램을 승격 합니다.

> [!NOTE]
> 준비 된 게시를 활성화 하려면 웹 응용 프로그램에 있어야 **표준 모드**합니다. Note를 표준 모드로 웹 앱을 변경 하는 경우 추가 비용이 발생에 발생 합니다. 가격에 대 한 자세한 내용은 참조 [앱 서비스 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)합니다.


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>1 – Azure 앱 서비스에서 웹 앱을 만드는 작업

이 태스크에서는의 웹 앱을 만들 **Azure 앱 서비스** 관리 포털에서 합니다. 또한 구성한는 **SQL 데이터베이스** 응용 프로그램 데이터를 유지 하 고 소스 제어에 대 한 로컬 Git 리포지토리를 구성 하려면.

1. 이동 하 여 [Azure 관리 포털](https://manage.windowsazure.com) 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.

    ![Azure 관리 포털에 로그인](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *Azure 관리 포털에 로그인*
2. 클릭 **새로** 페이지의 맨 아래에 명령 모음에서 합니다.

    ![새 웹 앱을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "새 웹 앱 만들기")

    *새 웹 앱 만들기*
3. 클릭 **계산**, **웹 사이트** 차례로 **사용자 지정 만들기**합니다.

    ![사용자 지정 만들기를 사용 하 여 새 웹 앱을 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기")

    *사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기*
4. 에 **새 웹 사이트-사용자 지정 만들기** 대화 상자를 사용 가능한 제공 **URL** (예: *들은 퀴즈*), 위치를 선택는 **영역** 드롭다운 목록 및 선택 **새 SQL 데이터베이스 만들기** 에 **데이터베이스** 드롭 다운 목록입니다. 마지막으로 선택 된 **소스 제어에서 게시** 확인란과 클릭 **다음**합니다.

    ![새 웹 앱을 사용자 지정](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *새 웹 앱을 사용자 지정*
5. 데이터베이스 설정에 대 한 다음 정보를 지정 합니다.

   - 에 **이름** 텍스트 상자에 데이터베이스 이름을 입력 합니다 (예: *geekquiz\_db*)
   - 서버에서 **드롭 다운** 목록에서 **새 SQL 데이터베이스 서버**합니다. 또는 기존 서버를 선택할 수 있습니다.
   - 에 **데이터베이스 사용자 이름** 및 **데이터베이스 암호** 상자 SQL 데이터베이스 서버에 대 한 관리자 사용자 이름 및 암호를 입력 합니다. 서버를 선택 하면 이미 만든 경우 암호를 묻는 메시지가 표시 됩니다.

     ![데이터베이스 설정 지정](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *데이터베이스 설정 지정*
6. **다음** 을 클릭하여 계속합니다.
7. 선택 **로컬 Git 리포지토리** 사용 하 고 클릭 하 여 소스 제어에 대 한 **다음**합니다.

    > [!NOTE]
    > 배포 자격 증명 (사용자 이름 및 암호)에 대 한 하 라는 메시지가 표시 될 수 있습니다.

    ![Git 리포지토리를 만드는 중](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *Git 리포지토리를 만드는 중*
8. 새 웹 앱을 만들 때까지 대기 합니다.

    > [!NOTE]
    > 기본적으로 Azure에서 도메인을 제공 *azurewebsites.net* 아니지만 Azure 관리 포털을 사용 하 여 사용자 지정 도메인을 설정 하려면 가능성도 제공 합니다. 그러나 특정 Azure 앱 서비스 모드를 사용 하는 경우 사용자 지정 도메인에 관리할 수만 있습니다.
    > 
    > Azure 앱 서비스는 무료, 공유, Basic, Standard 및 Premium edition에서 사용할 수 있습니다. 무료 및 공유 모드에서는 모든 웹 앱 다중 테 넌 트 환경에서 실행 하 고 CPU, 메모리 및 네트워크 사용량에 대 한 할당량이 합니다. 무료 앱의 최대 수는 계획 달라질 수 있습니다. 표준 모드에서는 표준 Azure에 해당 하는 전용된 가상 컴퓨터에서 실행 되는 앱 리소스를 계산 하는 것이 있습니다. 웹 응용 프로그램 모드 구성에서 찾을 수 있습니다는 **배율** 웹 응용 프로그램의 메뉴.
    > 
    > ![Azure 앱 서비스 모드](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure 앱 서비스 모드")
    > 
    > 사용 중인 경우 **Shared** 또는 **표준** 응용 프로그램으로 이동 하 여 웹 앱에 대 한 사용자 지정 도메인을 관리할 수 있는 모드 **구성** 를클릭하고메뉴**도메인 관리** 아래 *도메인 이름*합니다.
    > 
    > ![도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "도메인 관리")
    > 
    > ![사용자 지정 도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "사용자 지정 도메인 관리")
9. 웹 응용 프로그램을 만든 후 아래의 링크를 클릭는 **URL** 열을 새 웹 응용 프로그램이 실행 되 고 있는지 확인 합니다.

    ![새 웹 앱을 검색합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *새 웹 앱을 검색합니다.*

    ![웹 앱이 실행 중인](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *웹 앱이 실행 중인*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>작업 2-프로덕션 SQL 데이터베이스 만들기

이 작업을 사용 하 여는 **Entity Framework Code First 마이그레이션을** 를 대상으로 데이터베이스를 만들려면는 **Azure SQL 데이터베이스** 이전 태스크에서 만든 인스턴스.

1. 관리 포털에서 이전 태스크에서 만든 웹 앱으로 이동 하 고 이동 해당 **대시보드**합니다.
2. 에 **대시보드** 페이지 **연결 문자열 보기** 링크는 **눈에 보는** 섹션.

    ![연결 문자열 보기](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "연결 문자열 보기")

    *연결 문자열을 봅니다.*
3. 복사는 **연결 문자열** 값 및 대화 상자를 닫습니다.

    ![Azure 관리 포털에서 연결 문자열](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 관리 포털에서 연결 문자열")

    *Azure 관리 포털에서 연결 문자열*
4. 클릭 **SQL 데이터베이스** Azure의 SQL 데이터베이스의 목록을 보려면

    ![SQL 데이터베이스 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL 데이터베이스 메뉴")

    *SQL 데이터베이스 메뉴*
5. 이전 태스크에서 만든 데이터베이스를 찾아 서버의 클릭 합니다.

    ![SQL 데이터베이스 서버](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL 데이터베이스 서버")

    *SQL 데이터베이스 서버*
6. 에 **빠른 시작** 페이지에서 클릭 하 고 서버의 **구성**합니다.

    ![구성 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "구성 메뉴")

    *메뉴 구성*
7. 에 **허용 IP 주소** 섹션에서 클릭 **허용된 IP 주소에 추가** 링크 IP SQL 데이터베이스 서버에 연결 하는 데 사용할 수 있도록 합니다.

    ![허용 된 IP 주소](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "허용 IP 주소")

    *허용 된 IP 주소*
8. 클릭 **저장** 단계를 완료 하려면 페이지 맨 아래에 있습니다.
9. Visual Studio로 다시 전환 합니다.
10. 에 **패키지 관리자 콘솔**, 대체 하는 다음 명령을 실행 *[귀하가 연결 문자열]* Azure에서 복사한 연결 문자열과 함께 자리 표시자

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![Windows Azure SQL 데이터베이스를 대상으로 지정 된 데이터베이스 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL 데이터베이스를 대상으로 지정 된 데이터베이스 업데이트")

    *Azure SQL 데이터베이스를 대상으로 하는 데이터베이스를 업데이트 합니다.*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>작업 3 – Git를 사용 하 여 스테이징 배포 들은 퀴즈

이 태스크에서는 웹 응용 프로그램에서 준비 된 게시를 설정 합니다. 그런 다음는 들은 퀴즈 응용 프로그램을 게시할 로컬 컴퓨터에서 직접 웹 응용 프로그램의 스테이징 환경에 Git를 사용 합니다.

1. 대상 웹 응용 프로그램의 이름을 클릭 하 고 다시 포털로 이동는 **이름** 관리 페이지를 표시 하는 열입니다.

    ![웹 응용 프로그램 관리 페이지 열기](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *웹 응용 프로그램 관리 페이지 열기*
2. 로 이동 된 **배율** 페이지. 아래는 **일반** 섹션에서 **표준** 구성과 클릭에 대 한 **저장** 명령 모음에서 합니다.

    > [!NOTE]
    > 현재 지역 및 구독에서 모든 웹 앱을 실행 하려면 **표준** 모드, 범위 밖의 **모두 선택** 확인란을 선택는 **사이트 선택** 구성 합니다. 그렇지 않은 경우의 선택을 취소는 **모두 선택** 확인란 합니다.

    ![웹 앱을 표준 모드로 업그레이드](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "를 표준 모드로 웹 응용 프로그램 업그레이드")

    *웹 앱을 표준 모드로 업그레이드*
3. 클릭 **예** 하 여 변경 사항을 확인 합니다.

    ![표준 모드로 변경 내용을 확인](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "웹 응용 프로그램 모드를 변경 하 여 계속 합니다.")

    *표준 모드에 대 한 변경 확인*
4. 이동 하는 **대시보드** 페이지 클릭 하 여 **사용 준비 게시** 아래는 **눈에 보는** 섹션.

    ![준비 된 게시를 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "사용 하도록 설정 하면 게시 준비")

    *준비 된 게시를 사용 하도록 설정*
5. 클릭 **예** 준비 된 게시를 사용 하도록 합니다.

    ![준비 된 게시 확인](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "준비 된 게시를 사용 하도록 설정 하려면 예 클릭")

    *준비 된 게시를 확인합니다.*
6. 웹 응용 프로그램의 목록에서 준비 사이트 슬롯을 표시 하 여 웹 응용 프로그램 이름 왼쪽에 있는 표시를 확장 합니다. 다음 웹 앱 이름이 ***(준비)***합니다. 준비 사이트 관리 페이지로 이동 하려면 클릭 합니다.

    ![스테이징 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "스테이징 웹 앱으로 이동")

    *준비 응용 프로그램으로 이동*
7. 다른 모든 웹 앱의 관리 페이지 처럼 보이는 해당 그 관리 페이지를 확인 합니다. 로 이동 된 **배포** 페이지 및 복사는 **Git URL** 값입니다. 이 연습에서는 나중에 사용 합니다.

    ![Git URL 값 복사](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *Git URL 값 복사*
8. 새 **Git Bash** 콘솔을 통해 다음 명령을 실행 합니다. 업데이트는 *[귀하가 응용 프로그램 경로]* 자리 표시자에 대 한 경로 **GeekQuiz** 에 있는 솔루션의 **Source\Ex1 DeployingWebSiteToStaging\Begin** 의 폴더 이 랩에서 합니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 초기화 및 첫 번째 커밋](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git 초기화 및 첫 번째 커밋*
9. 원격 웹 앱 밀어 넣으려면 다음 명령을 실행 **Git** 저장소입니다. 관리 포털에서 가져온 URL 자리 표시자를 바꿉니다. 배포 암호를 묻는 메시지가 나타납니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure에 강제 설치](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *Azure에 강제 설치*

    > [!NOTE]
    > FTP 호스트 또는 웹 응용 프로그램의 GIT 리포지토리에 콘텐츠를 배포할 때 사용 하 여 인증 해야 합니다는 **배포 자격 증명** 웹 앱에서 만든 **빠른 시작** 또는 **대시보드**  관리 페이지입니다. 배포 자격 증명을 사용 하 여 알 수 없는 경우 관리 포털을 사용 하 여 쉽게 재설정할 수 있습니다. 웹 앱을 열고 **대시보드** 페이지를 클릭 하 고는 **배포 자격 증명 재설정** 링크 합니다. 새 암호를 입력 하 고 클릭 **확인**합니다. 배포 자격 증명은 구독과 연결 된 모든 웹 앱과 함께 사용 하기에 적합 합니다.
10. Azure에 성공적으로 푸시된 웹 앱을 확인 하기 위해 다시 관리 포털로 이동 하 고 클릭 **웹 사이트**합니다.
11. 웹 앱을 찾아 준비 사이트 슬롯을 표시 하려면 항목을 확장 합니다. 클릭 하 여 해당 **이름** 관리 페이지로 이동 합니다.
12. 클릭 **배포** 볼 수는 **배포 기록을**합니다. 되는지 확인 한 **활성 배포** 와 프로그램  *&quot;초기 커밋&quot;*합니다.

    ![활성 배포](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *활성 배포*
13. 마지막으로, 클릭 **찾아보기** 웹 앱으로 이동 하려면 명령 모음에서 합니다.

    ![웹 앱을 찾아보기](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *웹 앱을 찾아보기*
14. 응용 프로그램을 성공적으로 배포한 경우 들은 퀴즈 로그인 페이지가 표시 됩니다.

    > [!NOTE]
    > 배포 응용 프로그램의 주소 URL 뒤 웹 응용 프로그램의 이름을 포함 *-준비*합니다.

    ![스테이징 환경에서 실행 중인 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *스테이징 환경에서 실행 중인 응용 프로그램*
15. 클릭 하 여 응용 프로그램을 탐색 하려면 **등록** 에 새 사용자를 등록 합니다. 사용자 이름, 전자 메일 주소 및 암호를 입력 하 여 계정 세부 정보를 완료 합니다. 다음으로 응용 프로그램에서는 퀴즈의 첫 번째 질문을 보여 줍니다. 예상 대로 작동 하는지 확인 하는 몇 가지 질문에 답변 합니다.

    ![응용 프로그램을 사용할 준비가 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *응용 프로그램을 사용할 준비가 되었습니다.*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>작업 4-프로덕션 환경에 웹 응용 프로그램을 승격 합니다.

스테이징 환경에서 웹 응용 프로그램이 제대로 작동 하는지 확인 하 고 이제 프로덕션으로 승격할 준비가 되었습니다. 이 태스크에서는 됩니다 프로덕션 사이트 슬롯으로 준비 사이트 슬롯을 교체 합니다.

1. 관리 포털에 다시 이동 하 고 준비 사이트 슬롯을 선택 합니다. 클릭 **교체** 명령 모음에서 합니다.

    ![프로덕션 환경으로 교체 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *프로덕션 환경으로 교체 합니다.*
2. 클릭 **예** 확인 대화 상자에서는 스왑 작업을 진행할 수 있습니다. Azure 됩니다 즉시 준비 사이트의 내용 사용 하 여 프로덕션 사이트의 콘텐츠를 교체 합니다.

    > [!NOTE]
    > 준비 된 버전에서 일부 설정이 고 (예: 연결 문자열 재정의 처리기 매핑, 등), 프로덕션 버전에 자동으로 복사 될 수 있지만 (예: DNS 끝점, SSL 바인딩을 등)에 다른 설정은 변경 되지 않습니다.

    ![스왑 작업을 확인합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *스왑 작업을 확인합니다.*
3. 스왑 완료 되 면 프로덕션 슬롯을 선택 하 고 클릭 **찾아보기** 프로덕션 사이트를 열려면 명령 모음에서 합니다. 주소 표시줄에 URL을 확인 합니다.

    > [!NOTE]
    > 캐시를 지우려면 브라우저를 새로 고쳐야 할 수 있습니다. Internet Explorer에서 할 수 있는이 키를 눌러 **CTRL + R**합니다.

    ![프로덕션 환경에서 실행 되는 웹 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. 에 **GitBash** 콘솔에서 프로덕션 슬롯을 대상으로 로컬 Git 리포지토리에 대 한 원격 URL을 업데이트 합니다. 이 위해 웹 응용 프로그램의 이름 및 프로그램 배포 사용자 이름 자리 표시자를 바꾸는 다음 명령을 실행 합니다.

    > [!NOTE]
    > 다음 실습에서 랩의 단순성에 대 한 스테이징 대신 프로덕션 사이트에 변경 내용을 푸시합니다. 실제 시나리오에서 프로덕션으로 승격 하기 전에 스테이징 환경에 변경 내용을 확인 하는 것이 좋습니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>연습 3: 프로덕션 환경에서 배포 Rollback 수행

여기서 없는 핫 스왑 스테이징 및 프로덕션, 예를 들어 간에 수행 하려면 스테이징 슬롯으로 작업 하는 경우 시나리오 **무료** 또는 **Shared** 모드입니다. 이러한 시나리오에서 테스트 해야 테스트 환경에서 응용 프로그램-로컬 또는 원격 사이트에서-프로덕션 환경에 배포 하기 전에. 그러나 있기 테스트 단계에서 검색 되지 문제가 프로덕션 사이트에 발생할 수 있습니다. 이 경우 중요 한지 쉽게 응용 프로그램의 이전 및 더 안정 된 버전으로 최대한 빠르게 전환할 수 있는 메커니즘입니다.

**Azure 앱 서비스**, 소스 제어에서 연속 배포 수 가능한 덕분에이 기술을 사용 하면는 **재배포** 관리 포털에서 사용할 수 있는 작업입니다. Azure는 커밋이 리포지토리에 푸시와 관련 된 배포를 추적 하 고 이전 배포를 사용 하 여 언제 든 지 응용 프로그램을 다시 배포 하는 옵션을 제공 합니다.

이 연습에서 코드에 대 한 변경 수행는 **들은 퀴즈** 가 의도적으로 삽입 하는 응용 프로그램을 *버그*합니다. 오류를 확인 하려면 프로덕션 환경에 응용 프로그램을 배포 합니다 및 다음의 이전 상태로 돌아가는 재배포 기능 걸립니다.

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>작업 1-들은 퀴즈 응용 프로그램 업데이트

이 태스크의 코드의 작은 부분 리팩터링 됩니다는 **TriviaController** 클래스 새 메서드로 선택한 퀴즈 옵션은 데이터베이스에서 검색 하는 논리의 일부를 추출 합니다.

1. 사용 하 여 Visual Studio 인스턴스를 전환할는 **GeekQuiz** , 이전 연습에서 솔루션입니다.
2. **솔루션 탐색기**열고는 **TriviaController.cs** 내 파일의 **컨트롤러** 폴더입니다.
3. 찾을 **StoreAsync** 메서드와 코드는 다음 그림에 강조 표시 선택 합니다.

    ![코드를 선택합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *코드를 선택합니다.*
4. 확장 하 고, 선택한 코드를 마우스 오른쪽 단추로 클릭는 **리팩터링** 메뉴와 선택 **메서드 추출...** .

    ![새 메서드는 코드를 추출 하는 중](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *추출 방법 선택*
5. 에 **메서드 추출** 대화 상자에 새 메서드 이름 *MatchesOption* 클릭 **확인**합니다.

    ![메서드 이름 지정](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *추출 된 메서드에 대 한 이름 지정*
6. 그런 다음 선택한 코드 추출 되는 **MatchesOption** 메서드. 결과 코드는 다음 코드 조각에 표시 됩니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. 키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>작업 2-들은 퀴즈 응용 프로그램을 다시 배포

이제 프로덕션 환경에 새 배포를 트리거하는 리포지토리가 이전 태스크에서 변경한 내용을 푸시됩니다. 사용 하 여 문제가 문제 해결은 그런 다음는 **F12 개발 도구** Internet Explorer에서 제공 하 고 다음 Azure 관리 포털에서 롤백 이전 배포를 수행 합니다.

1. 새 **Git Bash** Azure 앱 서비스에 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.
2. Azure에 변경 내용을 푸시 하려면 다음 명령을 실행 합니다. 업데이트는 *[귀하가 응용 프로그램 경로]* 자리 표시자에 대 한 경로 **GeekQuiz** 솔루션입니다. 배포 암호를 묻는 메시지가 나타납니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Azure에 리팩터링된 코드를 강제 설치](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *Azure에 리팩터링된 코드를 강제 설치*
3. Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`). 이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.
4. 키를 눌러 **F12** 개발 도구를 시작 하려면는 **네트워크** 탭을 클릭는 **재생** 기록을 시작 하려면 단추입니다.

    ![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "네트워크 기록 시작")

    *네트워크 기록 시작*
5. 퀴즈의 옵션을 선택 합니다. 아무 작업도 수행 하는 것이 나타납니다.
6. 에 **F12** 창, 해당 POST HTTP 요청 하는 항목 표시 HTTP **500** 결과입니다.

    ![HTTP 500 오류](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 오류*
7. 선택 된 **콘솔** 탭 합니다. 오류 원인 세부 정보와 함께 기록 됩니다.

    ![기록 된 오류](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *기록 된 오류*
8. 오류 세부 정보 부분을 찾습니다. 명확 하 게,이 오류는 이전 단계에서 커밋된 하면 리팩터링 코드에 의해 발생 합니다.

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.
9. 브라우저를 닫지 마십시오.
10. 로 이동 하는 새 브라우저 인스턴스에서 [Azure 관리 포털](https://manage.windowsazure.com) 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.
11. 선택 **웹 사이트** 연습 2에서 만든 웹 응용 프로그램을 클릭 합니다.
12. 탐색 하 고 **배포** 페이지. 배포 기록에 모든 커밋을 수행에 나열 됩니다.

    ![기존 배포의 목록](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *기존 배포의 목록*
13. 이전의 커밋을 선택 하 고 클릭 **재배포** 명령 모음에서 합니다.

    ![이전의 커밋 다시 배포](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *이전의 커밋 다시 배포*
14. 를 확인 하 라는 메시지가 나타나면 클릭 **예**합니다.

    ![재배포를 확인합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. 웹 앱 및 키를 눌러 브라우저 인스턴스를 다시 배포 완료 되 면 전환 **CTRL + f 5를 눌러**합니다.
16. 옵션 중 하나를 클릭 합니다. 전체 및 결과 이제 플립 애니메이션 걸립니다 (*/오*) 표시 됩니다.
17. (선택 사항) 전환 하는 **Git Bash** 콘솔을 이전 커밋을로 되돌리려면 다음 명령을 실행 합니다.

    > [!NOTE]
    > 이러한 명령에 잘못 된 커밋의 Git 리포지토리 모든 변경 내용을 실행 취소 하는 새 커밋이 만듭니다. 다음 azure에는 새 커밋을 사용 하 여 응용 프로그램 다시 배포 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>연습 4: Azure 저장소를 사용 하 여 배율을

**Blob** 은 대량의 구조화 되지 않은 텍스트 또는 비디오, 오디오 및 이미지와 같은 이진 데이터를 저장 하는 가장 간단한 방법입니다. 저장소에 응용 프로그램의 정적 콘텐츠를 이동, 이미지 또는 브라우저에 직접 문서를 이용 하 여 응용 프로그램을 확장할 수 있습니다.

이 연습에서는 Blob 컨테이너에 응용 프로그램의 정적 콘텐츠를 이동 합니다. 다음 추가 하려면 응용 프로그램을 구성 합니다는 **ASP.NET URL 재작성 규칙** 에 **Web.config** Blob 컨테이너에 콘텐츠를 리디렉션할 수 있습니다.

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>작업 1 – Azure 저장소 계정 만들기

이 작업을 관리 포털을 사용 하 여 새 저장소 계정을 만드는 방법에 설명 합니다.

1. 로 이동 된 [Azure 관리 포털](https://manage.windowsazure.com) 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.
2. 선택 **새로 만들기 | 데이터 서비스 | 저장소 | 빠른 생성** 새 저장소 계정 만들기를 시작 합니다. 선택한 계정에 대 한 고유한 이름을 입력 한 **지역** 목록에서 합니다. 클릭 **저장소 계정 만들기** 를 계속 합니다.

    ![새 저장소 계정을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "새 저장소 계정 만들기")

    *새 저장소 계정 만들기*
3. 에 **저장소** 섹션에서 새 저장소 계정의 상태 바뀔 때까지 기다렸다가 *온라인* 다음 단계를 계속 하려면.

    ![만든 저장소 계정](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "만든 저장소 계정")

    *만든 저장소 계정*
4. 저장소 계정 이름을 클릭 한 다음 클릭는 **대시보드** 페이지 맨 아래에 링크 합니다. **대시보드** 페이지에서 계정과 응용 프로그램 내에서 사용할 수 있는 서비스 끝점의 상태에 대 한 정보를 제공 합니다.

    ![저장소 계정 대시보드에 표시](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "저장소 계정 대시보드를 표시 합니다.")

    *저장소 계정 대시보드를 표시합니다.*
5. 클릭는 **액세스 키 관리** 탐색 모음에서 단추입니다.

    ![선택 키 [관리] 단추](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "액세스 키 관리 단추")

    *관리 액세스 키 단추*
6. 에 **액세스 키 관리** 대화 상자, 복사는 **저장소 계정 이름** 및 **기본 액세스 키** 다음 연습에 필요한 합니다. 그런 다음 대화 상자를 닫습니다.

    ![관리 액세스 키 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "액세스 키 관리 대화 상자")

    *관리 액세스 키 대화 상자*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>작업 2-Azure Blob 저장소로 자산을 업로드 하는 중입니다.

이 작업에서는 저장소 계정에 연결 하는 데 Visual Studio에서 서버 탐색기 창을 사용 합니다. 그런 다음 blob 컨테이너를 만들고 들은 퀴즈 로고 파일을 컨테이너에 업로드 합니다.

1. 사용 하 여 Visual Studio 인스턴스를 전환할는 **GeekQuiz** , 이전 연습에서 솔루션입니다.
2. 메뉴 모음에서 선택 **보기** 클릭 하 고 **서버 탐색기**합니다.
3. **서버 탐색기**를 마우스 오른쪽 단추로 클릭는 **Azure** 노드 선택한 **Azure에 연결...** . 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.

    ![Windows Azure에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *Azure에 연결*
4. 확장 된 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **저장소** 선택 **외부 저장소 연결...** .
5. 에 **새 저장소 계정 추가** 대화 상자에 입력에서 **계정 이름** 및 **계정 키** 클릭 확인 하 고 이전 작업에서 얻은 **확인**.

    ![새 저장소 계정 대화 상자를 추가 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *새 저장소 계정 대화 상자를 추가 합니다.*
6. 저장소 계정 아래에 나타나야 합니다.는 **저장소** 노드. 저장소 계정의 확장 하 고 마우스 오른쪽 단추로 클릭 **Blob** 선택 **Blob 컨테이너 만들기...** .

    ![Blob 컨테이너 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob 컨테이너 만들기")

    *Blob 컨테이너 만들기*
7. 에 **Create Blob Container** 대화 상자, blob 컨테이너에 대 한 이름을 입력 하 고 클릭 **확인**합니다.

    ![Blob 컨테이너 대화 상자 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob 컨테이너 만들기 대화 상자")

    *Blob 컨테이너 대화 상자 만들기*
8. 새 blob 컨테이너에 추가 해야는 **Blob** 노드. 컨테이너를 공용 컨테이너에서 액세스 권한을 변경 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **이미지** 컨테이너와 선택 **속성**합니다.

    ![컨테이너 속성 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "컨테이너 속성 이미지")

    *컨테이너 속성 이미지*
9. 에 **속성** 창의 설정는 **공용 읽기 액세스 권한을** 를 **컨테이너**합니다.

    ![공용 읽기 권한 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "공용 읽기 권한 속성을 변경")

    *변경 되는 공용 읽기 권한 속성*
10. 공용 액세스 속성을 변경 하려면 대화 상자가 나타나면 확실치 **예**합니다.

    ![Microsoft Visual Studio 경고](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 경고")

    *Microsoft Visual Studio warning*
11. **서버 탐색기**를 마우스 오른쪽 단추로 클릭는 **이미지** blob 컨테이너 및 선택 **Blob 컨테이너 보기**합니다.

    ![Blob 컨테이너 보기](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob 컨테이너 보기")

    *Blob 컨테이너 보기*
12. 이미지 컨테이너가 해야 새 창에서 열고는 항목이 없으면 범례가 표시 되어야 합니다. 클릭는 **업로드** 아이콘 blob 컨테이너에 파일을 업로드 합니다.

    ![항목이 없는 이미지 컨테이너가](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "항목이 없는 컨테이너 이미지")

    *항목이 없는 컨테이너 이미지*
13. 에 **Blob 업로드** 대화 상자에서 이동 하는 **자산** 랩의 폴더입니다. 선택 된 **로고 big.png** 파일을 클릭 하 여 **열려**합니다.
14. 파일을 업로드할 때까지 기다립니다. 업로드가 완료 되 면 이미지 컨테이너에 파일을 나열 합니다. 파일 항목을 마우스 오른쪽 단추로 클릭 하 고 선택 **URL 복사**합니다.

    ![Blob URL을 복사](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "blob 파일 URL 복사")

    *Blob URL 복사*
15. Internet Explorer를 열고 URL을 붙여 넣습니다. 다음 이미지는 브라우저에 표시 되어야 합니다.

    ![Windows Blob 저장소에서 big.png 로고 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "저장소에서 big.png 로고 이미지")

    *Azure Blob 저장소에서 big.png 로고 이미지*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>작업 3 – Azure Blob 저장소에서 정적 콘텐츠를 사용할 솔루션을 업데이트 합니다.

이 태스크에서는 구성에서 **GeekQuiz** 이미지를 사용 하는 솔루션 Azure Blob 저장소에 업로드 (대신 웹 앱에 있는 이미지)에 ASP.NET URL 다시 쓰기 규칙을 추가 하 여는 **web.config**파일입니다.

1. Visual Studio에서 엽니다는 **Web.config** 내 파일의 **GeekQuiz** 프로젝트를 찾습니다는 **&lt;system.webServer&gt;** 요소입니다.
2. URL 재작성을 저장소 계정 이름 자리 표시자 업데이트 규칙을 추가 하려면 다음 코드를 추가 합니다.

    (코드 조각- *WebSitesInProduction-Ex4-UrlRewriteRule*)

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL 다시 쓰기는 들어오는 웹 요청을 가로채 고 다른 리소스에 요청을 리디렉션하는 과정입니다. 규칙을 다시 작성 하는 URL 다시 쓰기 엔진은 리디렉션해야 하 고 요청을 리디렉션할 수 필요로 하는 경우를 나타냅니다. 두 문자열의 다시 쓰기 규칙이 구성 됩니다: 요청한 URL에서 찾을 패턴 (일반적으로 사용 정규식) 하는 경우, 사용 하 여 패턴을 바꿀 문자열을 찾을 수 있습니다. 자세한 내용은 참조 [ASP.NET의 URL 다시 쓰기](https://msdn.microsoft.com/library/ms972974.aspx)합니다.
3. 키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.
4. 새 **Git Bash** Azure 앱 서비스에 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.
5. Azure에 변경 내용을 푸시 하려면 다음 명령을 실행 합니다. 업데이트는 *[귀하가 응용 프로그램 경로]* 자리 표시자에 대 한 경로 **GeekQuiz** 솔루션입니다. 배포 암호를 묻는 메시지가 나타납니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure에 업데이트 배포](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *Azure에 업데이트 배포*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>작업 4-확인

이 작업을 사용 하 여 **Internet Explorer** 검색 하는 **들은 퀴즈** URL 재작성 이미지 작동 하 고에 대 한 규칙을 확인 하 고 응용 프로그램에 호스팅된 이미지 리디렉션됩니다 **Azure Blob 저장소**합니다.

1. Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`). 이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.

    ![이미지와 들은 퀴즈 웹 앱을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "들은 퀴즈 웹 응용 프로그램을 이미지를 표시 합니다.")

    *이미지와 들은 퀴즈 웹 앱을 표시합니다.*
2. 키를 눌러 **F12** 개발 도구를 시작 하려면는 **네트워크** 탭 하 고 기록을 시작 합니다.

    ![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "네트워크 기록 시작")

    *네트워크 기록 시작*
3. 키를 눌러 **CTRL + f 5를 눌러** 웹 페이지를 새로 고쳐야 합니다.
4. HTTP 요청에 대 한 페이지 로드가 완료 되 면 나타납니다는 **/img/logo-big.png** HTTP URL **301** (리디렉션) 결과 및 다른 요청에 대 한 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` http URL**200** 결과입니다.

    ![URL 리디렉션 확인](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "리디렉션 개발 도구에 표시")

    *URL 리디렉션을 확인 하는 중*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>연습 5: 웹 앱에 대 한 자동 크기 조정 사용

> [!NOTE]
> 이 연습은 선택 사항이 웹 부하에 대 한 지원 하므로 &amp; 성능 테스트 에서만 사용할 수 있는 **Visual Studio 2013 Ultimate Edition**합니다. 대 한 자세한 내용은 특정 Visual Studio 2013 기능, 버전 비교 [여기](https://www.microsoft.com/visualstudio/eng/products/compare)합니다.


**Azure 앱 서비스 웹 앱** 실행 되는 웹 앱에 대 한 자동 크기 조정 기능을 제공 **표준 모드**합니다. 자동 크기 조정에는 부하에 따라 웹 응용 프로그램의 인스턴스 수를 자동으로 조정 수 있습니다. 자동 크기 조정을 사용 하는 Azure 웹 앱의 CPU가 5 분 마다 한 번 확인 하 고 해당 시점에 필요한 만큼 인스턴스가 추가 합니다. CPU 사용량이 낮은 경우 인스턴스가 제거 됩니다 두 시간 마다 한 번씩 웹 앱의 성능이 저하 되지 되도록 합니다.

구성 하는 데 필요한 단계를 진행 합니다이 연습에서는 **자동 크기 조정** 에 대 한 기능는 **들은 퀴즈** 웹 앱입니다. 인스턴스 업그레이드를 트리거할 응용 프로그램에서 충분 한 CPU 부하를 생성 하는 Visual Studio 부하 테스트를 실행 하 여이 기능을 확인 합니다.

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>작업 1-CPU 메트릭을 기반 구성 자동 크기 조정

이 작업에서는 연습 2에서 만든 웹 응용 프로그램에 대 한 자동 크기 조정 기능을 사용 하도록 설정 하려면 Azure 관리 포털을 사용 합니다.

1. 에 [Azure 관리 포털](https://manage.windowsazure.com/)선택, **웹 사이트** 연습 2에서 만든 웹 응용 프로그램을 클릭 합니다.
2. 로 이동 된 **배율** 페이지. 아래는 **용량** 섹션에서 **CPU** 에 대 한는 **메트릭 별 크기 조정** 구성 합니다.

    > [!NOTE]
    > CPU 별 크기 조정, Azure 응용 프로그램 CPU 사용량을 변경 하는 경우 사용 하는 인스턴스 수를 동적으로 조정 합니다.

    ![CPU 별 크기 조정 하도록 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "자동 크기 조정에 대 한 CPU 메트릭을 선택 합니다.")

    *CPU 별 크기 조정 선택*
3. 변경 된 **대상 CPU** 구성을 **20**-**40** %입니다.

    > [!NOTE]
    > 이 범위는 웹 앱에 대 한 평균 CPU 사용량을 나타냅니다. Azure는 추가 하거나이 범위에 웹 앱을 유지 하도록 인스턴스를 제거 합니다. 에 지정 된 최소 및 최대 크기 조정 시 사용 하는 인스턴스 수는 **인스턴스 수** 구성 합니다. 위 또는 해당 제한을 벗어나서 azure 이동 하지 않습니다.
    > 
    > 기본 **대상 CPU** 값은이 랩의 목적에 대해서만 수정 합니다. 작은 값으로 CPU 범위를 구성 하 여 적당 한 로드 응용 프로그램에 배치 되 면 자동 크기 조정 트리거로 기회를 늘리고 있습니다.

    ![대상 CPU 20%에서 40% 사이의 변경](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "20%에서 40% 사이의 CPU 대상 변경")

    *대상 CPU 20%에서 40% 사이의 변경*
4. 클릭 **저장** 변경 내용을 저장 하려면 명령 모음에서 합니다.

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>작업 2-부하 테스트를 Visual Studio와 함께

이제 **자동 크기 조정** 되었습니다 구성 만듭니다는 **웹 성능 및 부하 테스트 프로젝트** 웹 앱에서 일부 CPU 부하를 생성 하기 위해 Visual Studio에서 합니다.

1. 열기 **Visual Studio Ultimate 2013** 선택 **파일 | 새로 만들기 | 프로젝트...**  새 솔루션을 시작 합니다.

    ![새 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
2. 에 **새 프로젝트** 대화 상자에서 **웹 성능 및 부하 테스트 프로젝트** 아래는 **Visual C# | 테스트** 탭 합니다. 있는지 확인 **.NET Framework 4.5** 은 프로젝트의 이름을 선택 하면 *WebAndLoadTestProject*, 선택는 **위치** 클릭 **확인**합니다.

    ![새 웹과 부하 테스트 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "새 웹과 부하 테스트 프로젝트 만들기")

    *새 웹과 부하 테스트 프로젝트 만들기*
3. 에 **WebTest1.webtest** 마우스 오른쪽 단추로 클릭는 **WebTest1** 노드와 클릭 **요청 추가**합니다.

    ![WebTest1에 요청 추가](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "WebTest1에 요청 추가")

    *WebTest1에 요청 추가*
4. 에 **속성** 창 새 요청 노드의 업데이트는 **Url** 웹 앱의 URL을 가리키도록 속성 (예: *[ http://geek-quiz.azurewebsites.net/ ](http://geek-quiz.azurewebsites.net/)*).

    ![Url 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url 속성을 변경")

    *Url 속성을 변경*
5. 에 **WebTest1.webtest** 창을 마우스 오른쪽 단추로 클릭 **WebTest1** 클릭 **루프 추가...** .

    ![WebTest1에 루프 추가](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "WebTest1에 루프 추가")

    *WebTest1에 루프 추가*
6. 에 **루프에 조건부 규칙 추가 및 항목** 대화 상자는 **For 루프** 규칙 및 다음과 같은 속성을 수정 합니다.

   1. **종료 하는 값:** 1000
   2. **컨텍스트 매개 변수 이름:** 반복기
   3. **증분 값:** 1

      ![For 루프 규칙을 선택 하 고 속성 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For 루프 규칙을 선택 하 고 속성 업데이트")

      *For 루프 규칙을 선택 하 고 속성 업데이트*
7. 아래는 **루프의 항목** 섹션에서 루프에 대 한 첫 번째 및 마지막 항목 하기 위해 이전에 만든 요청을 선택 합니다. 계속하려면 **확인** 을 클릭합니다.

    ![루프에 대 한 첫 번째 및 마지막 항목을 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "루프에 대 한 첫 번째 및 마지막 항목 선택")

    *루프에 대 한 첫 번째 및 마지막 항목 선택*
8. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **WebAndLoadTestProject** 프로젝트를 확장 하 고는 **추가** 메뉴와 선택 **부하 테스트 중...** .

    ![부하 테스트 프로젝트에 추가 WebAndLoadTestProject](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject 프로젝트에 부하 테스트를 추가 합니다.")

    *WebAndLoadTestProject 프로젝트에 부하 테스트를 추가합니다.*
9. 에 **부하 테스트 새로 만들기 마법사** 대화 상자를 클릭 **다음**합니다.

    ![새 부하 테스트 마법사](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "부하 테스트 새로 만들기 마법사")

    *부하 테스트 새로 만들기 마법사*
10. 에 **시나리오** 페이지에서 **대기 시간을 사용 하지 않는** 클릭 **다음**합니다.

    ![대기 시간을 사용 하지 않는 Selecting](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "를 대기 시간을 사용 하지 않는 선택")

    *인지 시간 사용을 선택 하면*
11. 에 **부하 패턴** 페이지에서 다음 사항을 확인는 **일정 부하** 옵션을 선택 합니다. 변경의 **사용자 수** 설정을 **250** 사용자 및 클릭 **다음**합니다.

    ![사용자 수가 250으로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "250 사용자 수를 변경 합니다.")

    *사용자 수가 250으로 변경*
12. 에 **테스트 조합 모델** 페이지에서 **순차적 테스트 순서 기반** 클릭 **다음**합니다.

    ![테스트 조합 모델을 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "테스트 조합 모델 선택")

    *테스트 조합 모델 선택*
13. 에 **테스트 조합 모델** 페이지 **추가 중...**  조합에 테스트를 추가 합니다.

    ![테스트 조합에 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "테스트 조합에 테스트 추가")

    *테스트 조합에 테스트 추가*
14. 에 **테스트 추가** 대화 상자를 두 번 클릭 **WebTest1** 테스트를 추가 하는 **선택한 테스트** 목록입니다. 계속하려면 **확인** 을 클릭합니다.

    ![WebTest1 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "WebTest1 테스트 추가")

    *WebTest1 테스트 추가*
15. 에 **테스트 조합** 페이지 **다음**합니다.

    ![완료 테스트 조합 페이지](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "완료 테스트 조합 페이지")

    *완료 테스트 조합 페이지*
16. 에 **네트워크 조합** 페이지 **다음**합니다.

    ![네트워크 조합 페이지에서 다음 클릭 하면](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "네트워크 조합 페이지에서 다음 클릭")

    *네트워크 조합 페이지에서 다음을 클릭 하면*
17. 에 **브라우저 조합** 페이지에서 **Internet Explorer 10.0** 브라우저의 종류와 클릭으로 **다음**합니다.

    ![브라우저 종류를 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "브라우저 종류를 선택 합니다.")

    *브라우저 종류를 선택합니다.*
18. 에 **카운터 집합** 페이지 **다음**합니다.

    ![카운터 집합 페이지에서 다음을 클릭 하](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "카운터 집합 페이지에서 다음 클릭")

    *카운터 집합 페이지에서 다음을 클릭 하면*
19. 에 **실행 설정** 페이지에서 설정는 **부하 테스트 지속 시간** 를 **5 분** 클릭 **마침**합니다.

    ![부하 테스트 지속 시간을 5 분으로 설정](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "부하 테스트 지속 시간을 5 분으로 설정")

    *부하 테스트 지속 시간을 5 분으로 설정*
20. **솔루션 탐색기**, 두 번 클릭은 **Local.settings** 테스트 설정을 탐색 하는 파일입니다. 기본적으로 Visual Studio 테스트를 실행 하려면 로컬 컴퓨터를 사용 합니다.

    > [!NOTE]
    > 또는 테스트 프로젝트를 사용 하 여 클라우드 부하 테스트 실행을 구성할 수 **온라인 VSO (Visual Studio)**합니다. VSO는 클라우드 기반 부하 테스트 좀 더 현실적인 부하를 시뮬레이션 하는 서비스, 보다 큰 CPU 용량, 사용 가능한 메모리 및 네트워크 대역폭을 같은 로컬 환경 제약 조건은 방지를 제공 합니다. VSO를 사용 하 여 부하 테스트를 실행 하는 방법에 대 한 자세한 내용은 참조 [이 여기서](https://www.visualstudio.com/get-started/load-test-your-app-vs)합니다.

    ![테스트 설정](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>작업 3-자동 크기 조정 확인

이제 이전 태스크에서 만든 부하 테스트를 실행 하 고 웹 앱 부하 상태에서 어떻게 적용 되는지 확인 합니다.

1. **솔루션 탐색기**를 두 번 클릭 **LoadTest1.loadtest** 를 부하 테스트를 엽니다.

    ![LoadTest1.loadtest 열기](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "LoadTest1.loadtest 열기")

    *LoadTest1.loadtest 열기*
2. 에 **LoadTest1.loadtest** 창에서 부하 테스트를 실행 하려면 도구 상자에서 첫 번째 단추를 클릭 합니다.

    ![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "부하 테스트 실행")

    *부하 테스트 실행*
3. 부하 테스트가 완료 될 때까지 기다립니다.

    > [!NOTE]
    > 부하 테스트 요청을 보내는 웹 앱에 동시에 여러 사용자가 시뮬레이션 합니다. 테스트가 실행 되는 경우에 모든 오류, 경고 또는 부하 테스트 실행에 관련 된 기타 정보를 검색 하는 사용 가능한 카운터를 모니터링할 수 있습니다.

    ![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "부하 테스트가 완료 될 때까지 대기")

    *부하 테스트 실행*
4. 테스트가 완료 되 면 관리 포털으로 돌아가서를 탐색 하는 **배율** 웹 응용 프로그램의 페이지입니다. 아래는 **용량** 섹션을 표시 되어야 그래프의 새 인스턴스를 자동으로 배포 되었습니다.

    ![새 인스턴스를 자동으로 배포](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *새 인스턴스를 자동으로 배포*

    > [!NOTE]
    > 변경 내용을 그래프에 표시 하려면 몇 분 정도 걸릴 수 있습니다 (키를 눌러 **CTRL + f 5를 눌러** 주기적으로 페이지를 새로). 변경 내용을 표시 되지 않으면 다음을 시도할 수 있습니다.
    > 
    > - 부하 테스트의 기간을 늘려야 (예: **10 분**)
    > - 최대값과 최소값을 줄이려면는 **대상 CPU** 웹 응용 프로그램의 자동 크기 조정 구성에 대 한 범위
    > - 부하 테스트와 클라우드에서 실행 **Visual Studio Online**합니다. 자세한 내용은 [여기](https://www.visualstudio.com/get-started/load-test-your-app-vs.aspx)

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서 설정 하 고 프로덕션 웹 앱을 Azure에 응용 프로그램을 배포 하는 방법을 배웠습니다. 검색 하 고 사용 하 여 데이터베이스를 업데이트 하 여 시작 **Entity Framework Code First 마이그레이션을**, 새 버전을 사용 하 여 사이트를 배포 하 여 계속 **Git** 롤백 수행 하는 안정적인 최신 버전의 사이트입니다. 또한 Blob 컨테이너에 정적 콘텐츠를 이동 하려면 저장소를 사용 하 여 앱의 크기를 조정 하는 방법을 배웠습니다.
