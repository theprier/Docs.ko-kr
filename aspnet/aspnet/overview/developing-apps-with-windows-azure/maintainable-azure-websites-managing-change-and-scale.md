---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: '실습: Azure Websites 유지: 변경 및 확장 관리 | Microsoft Docs'
author: rick-anderson
description: 이 실습에서는 어떻게 Microsoft Azure를 쉽게 빌드하고 프로덕션으로 웹 사이트를 배포에 대해 알아봅니다.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: bc6de2f0c8b2cd958c198abb90fc4ad97613e973
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48913309"
---
<a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>실습: Azure Websites 유지: 변경 및 규모 관리
====================
[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](http://aka.ms/webcamps-training-kit)

> Microsoft Azure를 통해 쉽게 빌드 및 프로덕션 환경에 웹 사이트를 배포 합니다. 응용 프로그램 라이브 되 면 완료 되지 않았음을 있습니다 하지만 하면 이제 막 시작! 변경 요구 사항, 데이터베이스 업데이트, 확장성 등을 처리 해야 합니다. 다행 스럽게도 Azure App Service에서는 다양 한 원활 하 게 실행 하 여 사이트를 유지 하는 데 유용한 기능을 사용 하 여 설명 합니다.
>
> Azure는 안전 하 고 유연한 개발, 배포 및 확장 크기 웹 응용 프로그램에 대 한 옵션을 제공 합니다. 만들기 및 배포 인프라를 관리 해야 하는 번거로움 없이 응용 프로그램에 기존 도구를 활용 합니다.
>
> 프로 비전 프로덕션 웹 응용 프로그램을 직접 몇 분 안에 쉽게 하므로 좋아하는 개발 도구를 사용 하 여 만든 콘텐츠를 배포 하 여 합니다. 에 대 한 지원과 함께 소스 제어에서 직접 기존 사이트를 배포할 수 있습니다 **Git**, **GitHub**합니다 **Bitbucket**를 **TFS**, 및도  **DropBox**합니다. 사용 하 여 스크립트 또는 즐겨 찾는 IDE에서 직접 배포할 **PowerShell** Windows에서 또는 **CLI** 모든 OS에서 실행 되는 도구입니다. 을 배포한 후에 사이트를 연속 배포에 대 한 지원을 지속적으로 최신 상태로 유지 합니다.
>
> Azure 큰 또는 작은 모든 데이터에 대해 확장 가능한 지속형 클라우드 저장소, 백업 및 복구 솔루션 제공합니다. 프로덕션 환경에서 테이블, Blob 및 SQL Database와 같은 저장소 서비스를 응용 프로그램을 배포할 때 클라우드에서 응용 프로그램을 확장 하는 데 도움이 됩니다.
>
> SQL Database를 사용 하 여 응용 프로그램의 새 버전을 배포 하는 경우 생산성 데이터베이스를 최신 상태로 유지 하는 것이 반드시 합니다. 에 감사 드립니다 **Entity Framework Code First 마이그레이션을**, 개발 및 데이터 모델의 배포 환경을 몇 분 안에 업데이트 간소화 되었습니다. 이 실습 랩에서 Microsoft Azure에서 프로덕션 환경에 웹 앱을 배포할 때 발생할 수 있습니다 다른 항목에 표시 됩니다.
>
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.
>
> 이 항목의 자세한 자세한 검사를 참조 하세요. 합니다 [전자책은 Azure를 사용 하 여 실제 클라우드 앱 빌드](building-real-world-cloud-apps-with-windows-azure/introduction.md)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 기존 모델을 사용 하 여 Entity Framework 마이그레이션을 사용 하도록 설정
- 개체 모델 및 그에 따라 Entity Framework 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.
- Git를 사용 하 여 Azure App Service에 배포
- Azure 관리 포털을 사용 하 여 이전 배포로 롤백
- Azure Storage를 사용 하 여 웹 앱 확장
- Azure 관리 포털을 사용 하 여 웹 앱에 대 한 자동 크기 조정 구성
- 만들기 및 Visual Studio에서 부하 테스트 프로젝트 구성

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음는이 실습을 완료 해야 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상
- [Azure SDK for.NET 2.2](https://www.microsoft.com/windowsazure/sdk/)
- [GIT 버전 제어 시스템입니다.](http://git-scm.com/download)
- Microsoft Azure 구독

    - 등록을 [무료 평가판](http://aka.ms/watk-freetrial)
    - 인 경우 Visual Studio Professional, Test Professional, Premium 또는 Ultimate with MSDN 또는 MSDN 플랫폼 구독자를 활성화 하 [MSDN 혜택](http://aka.ms/watk-msdn) 개발 및 Azure에서 테스트를 시작 하려면 지금
    - [BizSpark](http://aka.ms/watk-bizspark) Azure를 자동으로 수신 하는 멤버는 Visual Studio Ultimate with MSDN subscription을 통해 혜택
    - 멤버는 [Microsoft Partner Network](http://aka.ms/watk-mpn) Cloud Essentials 프로그램에는 무료로 월간 Azure 크레딧 수신

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.

1. Windows 탐색기를 열고 실습용 **원본** 폴더입니다.
2. 마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택한 **관리자 권한으로 실행** 환경을 구성 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치는 설치 프로세스를 시작 합니다.
3. 사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각 사용

랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다. 사용자 편의 위해이 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

> [!NOTE]
> 각 실습에 시작 솔루션을 함께 표시 됩니다는 **시작** 다른 독립적으로 각 연습에 따라 할 수 있는 연습 하는 폴더입니다. 주의 하십시오 연습 하는 동안 추가 되는 코드 조각은 솔루션부터 이러한 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다. 연습에 대 한 소스 코드 안에 있습니다.는 **최종** 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션에 포함 된 폴더입니다. 이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [Entity Framework 마이그레이션을 사용 하 여](#Exercise1)
2. [스테이징 웹 앱 배포](#Exercise2)
3. [프로덕션 환경에서 배포 롤백 수행](#Exercise3)
4. [Azure Storage를 사용 하 여 확장](#Exercise4)
5. [웹 앱에 대 한 자동 크기 조정을 사용할](#Exercise5) (Visual Studio 2013 Ultimate edition에 대 한 선택 사항)

이 랩을 완료 하기 위한 예상 시간: **75 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>연습 1: Entity Framework 마이그레이션을 사용 하 여

응용 프로그램을 개발 하는 경우 데이터 모델에는 시간이 지남에 따라 변경 될 수 있습니다. (새 버전을 만들면) 하는 경우 이러한 변경 내용은 기존 모델 데이터베이스에 영향을 줄 수 및 데이터베이스를 오류를 방지 하려면 최신 상태로 유지 해야 합니다.

이러한 변경 내용 모델에 대 한 추적을 간소화 하기 위해 **Entity Framework Code First 마이그레이션을** 자동으로 데이터베이스 스키마를 사용 하 여 모델을 비교 하는 변경 내용을 검색 하 고 데이터베이스를 업데이트 하는 특정 코드를 생성 합니다. 새로 만들기 *버전* 데이터베이스입니다.

이 연습을 사용 하도록 설정 하는 방법을 보여 줍니다. **마이그레이션을** 응용 프로그램에 쉽게 검색 하는 방법에 데이터베이스를 업데이트 하려면 변경 내용을 생성 합니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>작업 1-마이그레이션 사용 하도록 설정

이 태스크를 사용 하도록 설정 하는 단계를 이동 **Entity Framework Code First 마이그레이션을** 에 **Geek 퀴즈** 데이터베이스, 모델을 변경 하 고에서 이러한 변경 내용이 반영 하는 방법을 이해 합니다 데이터베이스입니다.

1. Visual Studio를 열고 엽니다는 **GeekQuiz.sln** 에서 솔루션 파일 **Source\Ex1 UsingEntityFrameworkMigrations\Begin**합니다.
2. 다운로드 및 설치 하기 위해 솔루션을 구축 합니다 **NuGet** 종속성 패키지 합니다. 이렇게 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **솔루션 빌드** 누르거나 **Ctrl + Shift + B**합니다.
3. **도구** Visual Studio에서 메뉴 **NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.
4. 에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다. 기존 모델을 기반으로 하는 초기 마이그레이션 만들어질 수 있습니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![마이그레이션을 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "마이그레이션을 사용 하도록 설정")

    *마이그레이션을 사용 하도록 설정*

    > [!NOTE]
    > 이 명령은 추가 **마이그레이션을** Geek 퀴즈 프로젝트 파일이 포함 된 폴더의 이름은 **Configuration.cs**합니다. 합니다 **구성** 클래스를 사용 하면 마이그레이션에 대해 동작 하는 방식을 구성할 수 있습니다.
5. 마이그레이션을 사용 하도록 설정 된 업데이트 해야 합니다 **구성** 초기 데이터를 사용 하 여 데이터베이스를 채우는 데 클래스는 **Geek 퀴즈** 필요 합니다. 아래 **마이그레이션을**, 대체를 **Configuration.cs** 것을 사용 하 여 파일에는 **Source\Assets** 이 랩의 폴더입니다.

    > [!NOTE]
    > 이후 **마이그레이션을** 를 호출 합니다를 **초기값** 레코드가 데이터베이스에서 중복 되지 않았는지 확인 해야 하는 모든 데이터베이스 업데이트를 사용 하 여 메서드를 합니다. 합니다 **AddOrUpdate** 메서드 중복 데이터 방지 하는 데 도움이 됩니다.
6. 초기 마이그레이션에 추가 하려면 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.

    > [!NOTE]
    > 라는 데이터베이스가 있는지 확인 하십시오 &quot;GeekQuizProd&quot; LocalDB 인스턴스에 있습니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![기본 스키마 마이그레이션 추가](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "추가 기본 스키마 마이그레이션")

    *기본 스키마 마이그레이션 추가*

    > [!NOTE]
    > **Add-migration** 마지막 마이그레이션을 만든 후 모델에 대 한 변경 내용에 따라 다음 마이그레이션을 스 캐 폴딩 됩니다. 이 경우 첫 번째 마이그레이션 프로젝트의 경우 스크립트에 정의 된 모든 테이블을 만들려면 추가 됩니다는 **TriviaContext** 클래스입니다.
7. 다음 명령을 실행 하 여 데이터베이스를 업데이트 하려면 마이그레이션을 실행 합니다. 이 명령에 대 한 지정 된 **Verbose** 대상 데이터베이스에 적용 되 고 SQL 문을 보려면 플래그 합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![초기 데이터베이스 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "초기 데이터베이스 만들기")

    *초기 데이터베이스 만들기*

    > [!NOTE]
    > **Update-database** 마이그레이션을 보류 중인 데이터베이스에 적용 됩니다. 이 경우 web.config 파일에 정의 된 연결 문자열을 사용 하 여 데이터베이스가 만들어집니다.
8. 로 이동 **뷰** 메뉴를 열고 **SQL Server 개체 탐색기**합니다.

    ![SQL Server 개체 탐색기에서 열기](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server 개체 탐색기에서 열기")

    *SQL Server 개체 탐색기에서 열기*
9. 에 **SQL Server 개체 탐색기** 창 마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스에 연결 합니다 **SQL Server** 노드와 선택 **SQL Server 추가...**  옵션입니다.

    ![SQL Server 인스턴스를 추가](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server 인스턴스를 추가 합니다.")

    *SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*
10. 설정 합니다 **서버 이름** 하 *(localdb) \v11.0* 두고 **Windows 인증** 을 인증 모드로 합니다. 클릭 **Connect** 를 계속 합니다.

    ![LocalDB에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB에 연결")

    *LocalDB에 연결*
11. 엽니다는 **GeekQuizProd** 데이터베이스 및 확장을 **테이블** 노드. 알 수 있듯이 합니다 **Update-database** 명령에 정의 된 모든 테이블을 생성 합니다 **TriviaContext** 클래스입니다. 찾을 **dbo입니다. TriviaQuestions** 테이블 및 열 노드를 엽니다. 다음 태스크에서는이 테이블에 새 열을 추가 사용 하 여 데이터베이스를 업데이트할 **마이그레이션을**합니다.

    ![기타 정보 열 질문](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "퀴즈 질문 열")

    *기타 정보 열 질문*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>작업 2-마이그레이션을 사용 하 여 데이터베이스 스키마를 업데이트

이 태스크에서는 사용할지 **Entity Framework Code First 마이그레이션을** 모델에서 변경을 감지 하 여 데이터베이스를 업데이트 하는 데 필요한 코드를 생성 합니다. 업데이트를 **TriviaQuestions** 새 속성을 추가 하 여 엔터티. 다음 표에 새 열을 포함할 새 마이그레이션을 만들려면 명령을 실행 합니다.

1. **솔루션 탐색기**를 두 번 클릭 합니다 **TriviaQuestion.cs** 내에 있는 파일을 **모델** 폴더.
2. 라는 새 속성을 추가할 **힌트**다음 코드 조각에 나와 있는 것 처럼 합니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. 에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다. 모델의 변경을 반영 새 마이그레이션을 생성 됩니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![Add-migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-migration")

    *추가 마이그레이션*

    > [!NOTE]
    > 두 가지 방법으로 구성 된 마이그레이션 파일 **위로** 하 고 **아래로**합니다.
    >
    > - 합니다 **등록** 메서드를 사용 하 여 현재 버전의 데이터베이스에 적용 하는 응용 프로그램 요구 변경 내용 지정할 수는 있습니다.
    > - **아래로** 에 추가 변경을 하는 데 사용 되는 **위로** 메서드.
    >
    > 타임 스탬프 순서 및 해당 하는 마지막 업데이트 이후 사용 되지 않은 모든 마이그레이션을 데이터베이스 마이그레이션은 데이터베이스를 업데이트할 때 실행 됩니다 (의 \_마이그레이션을 적용 된 MigrationHistory 테이블의 추적). 합니다 **등록** 모든 마이그레이션 메서드의 호출 되며 지정한 데이터베이스에 변경 합니다. 마이그레이션 이전으로 돌아가서 하기로 하는 경우는 **다운** 메서드를 호출 하 여 역순으로 변경 내용을 다시 실행 하는 합니다.
4. 에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. 출력을 **Update-database** 생성 된 명령을 **Alter Table** SQL 문을 새 열을 추가 하는 **TriviaQuestions** 아래 이미지에 표시 된 대로 테이블입니다.

    ![추가 열 SQL 문을 생성](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "열 SQL 문을 생성 추가")

    *추가 열 SQL 문 생성*
6. **SQL Server 개체 탐색기**, 새로 고침을 **dbo입니다. TriviaQuestions** 테이블 및 확인 하는 새 **힌트** 열이 표시 됩니다.

    ![새 힌트 열을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "새 힌트 열 표시")

    *새 힌트 열 표시*
7. 다시 합니다 **TriviaQuestion.cs** 편집기를 추가 **StringLength** 제약 조건을 *힌트* 속성을 다음 코드 조각에 표시 된 대로 합니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. 에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. 에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. 출력을 **Update-database** 생성 된 명령을 **Alter Table** SQL 문을 업데이트를 *힌트* 열 유형의 **TriviaQuestions** 테이블을 아래 그림과에서 같이 합니다.

    ![Alter column SQL 문 생성](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 문 생성")

    *Alter column SQL 문 생성*
11. **SQL Server 개체 탐색기**, 새로 고침을 **dbo입니다. TriviaQuestions** 테이블 및 있는지 여부를 확인 합니다 **힌트** 열 형식이 **nvarchar(150)** 합니다.

    ![새 제약 조건을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "새 제약 조건을 보여 주는")

    *새 제약 조건을 보여 주는*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>연습 2: 스테이징 웹 앱 배포

**Azure App Service의 웹 앱** 스테이징 된 게시를 수행할 수 있습니다. 스테이징 된 게시 각 기본 프로덕션 사이트에 대 한 스테이징 사이트 슬롯을 만들고 중단 시간 없이 이러한 슬롯을 교환할 수 있습니다. 공개적으로 해제 하기 전에 변경 내용 유효성 검사, 증분 방식으로 사이트 콘텐츠를 통합 하 고 변경 내용이 예상 대로 작동 하지 않는 경우 롤백하지 데 매우 유용 합니다.

이 연습에서는 배포 합니다 **Geek 퀴즈** Git 소스 제어를 사용 하 여 웹 앱의 스테이징 환경에 응용 프로그램입니다. 이 위해 하면 웹 앱 만들기 및 관리 포털에서 필수 구성 요소를 프로 비전을 구성 된 **Git** 리포지토리 및 강제 응용 프로그램에서에서 소스 코드를 로컬 컴퓨터에서 스테이징 슬롯입니다. 또한 사용 하 여 프로덕션 데이터베이스를 업데이트 합니다 **Code First 마이그레이션을** 이전 연습에서 만든 합니다. 그런 다음 해당 작업을 확인 하려면이 테스트 환경에서 응용 프로그램을 실행 합니다. 만족 한다면 기대치에 따라 작동 하, 프로덕션 응용 프로그램을 승격 합니다.

> [!NOTE]
> 스테이징 된 게시를 사용 하려면 웹 앱에 있어야 **표준 모드**합니다. 표준 모드에 웹 앱을 변경 하면 추가 요금이 발생는 note 합니다. 가격 책정에 대 한 자세한 내용은 참조 하세요. [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)합니다.


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>작업 1-Azure App Service에서 웹 앱 만들기

이 작업에서 웹 앱을 만듭니다 **Azure App Service** 관리 포털에서 합니다. 구성도 **SQL Database** 응용 프로그램 데이터를 유지 하 고 소스 제어에 대 한 로컬 Git 리포지토리를 구성 하 합니다.

1. 로 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com) 구독과 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.

    ![Azure 관리 포털에 로그인](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *Azure 관리 포털에 로그인*
2. 클릭 **새로 만들기** 페이지의 맨 위에 있는 명령 모음에서.

    ![새 웹 앱을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "새 웹 앱 만들기")

    *새 웹 앱 만들기*
3. 클릭 **계산**하십시오 **웹 사이트** 차례로 **사용자 지정 만들기**합니다.

    ![사용자 지정 만들기를 사용 하 여 새 웹 앱을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기")

    *사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기*
4. 에 **새 웹 사이트-사용자 지정 만들기** 대화 상자에서 사용할 수 있는 제공 **URL** (예: *geek 퀴즈*), 위치를 선택 합니다 **지역** 드롭다운 목록에서 선택한 **새 SQL 데이터베이스를 만듭니다** 에 **데이터베이스** 드롭 다운 목록. 마지막으로 선택 합니다 **소스 제어에서 게시** 확인란을 클릭 **다음**합니다.

    ![새 웹 앱을 사용자 지정](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *새 웹 앱을 사용자 지정*
5. 데이터베이스 설정에 대 한 다음 정보를 지정 합니다.

   - 에 **이름을** 텍스트 상자에 데이터베이스 이름을 입력 합니다 (예: *geekquiz\_db*)
   - 서버에서 **드롭 다운** 목록에서 **새 SQL 데이터베이스 서버**합니다. 또는 기존 서버를 선택할 수 있습니다.
   - 에 **데이터베이스 사용자 이름** 하 고 **데이터베이스 암호** SQL database 서버에 대 한 관리자 사용자 이름 및 암호를 입력 하는 상자입니다. 서버를 선택 하면 이미 만든 경우 암호를 묻는 합니다.

     ![데이터베이스 설정 지정](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *데이터베이스 설정 지정*
6. **다음** 을 클릭하여 계속합니다.
7. 선택 **로컬 Git 리포지토리** 클릭 하 여 사용 하 여 소스 제어에 대 한 **다음**합니다.

    > [!NOTE]
    > 배포 자격 증명 (사용자 이름 및 암호) 하 라는 메시지가 표시 될 수 있습니다.

    ![Git 리포지토리를 만드는 중](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *Git 리포지토리를 만드는 중*
8. 새 웹 앱을 만들 때까지 기다립니다.

    > [!NOTE]
    > 기본적으로 Azure에서 도메인을 제공 *azurewebsites.net* 를 Azure 관리 포털을 사용 하 여 사용자 지정 도메인을 설정할 제공 합니다. 그러나 특정 Azure App Service 모드를 사용 하는 경우 사용자 지정 도메인에 관리할 수만 있습니다.
    >
    > Azure App Service는 Free, Shared, Basic, Standard 및 Premium edition에서 사용할 수 있습니다. 무료 및 공유 모드에서 모든 web apps 다중 테 넌 트 환경에서 실행 되며 CPU, 메모리 및 네트워크 사용량에 대 한 할당량을 갖습니다. 무료 앱의 최대 수는 계획을 사용 하 여 달라질 수 있습니다. 표준 모드에서 표준 Azure에 해당 하는 전용 가상 머신에서 실행 되는 앱 리소스를 계산 하는 것이 있습니다. 웹 앱 모드 구성에서 찾을 수 있습니다 합니다 **확장** 웹 앱의 메뉴.
    >
    > ![Azure App Service 모드](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 모드")
    >
    > 사용 중인 경우 **Shared** 또는 **표준** 앱으로 이동 하 여 웹 앱에 대 한 사용자 지정 도메인을 관리할 수 있는 모드 **구성** 메뉴와 클릭**도메인 관리** 아래에서 *도메인 이름*합니다.
    >
    > ![도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "도메인 관리")
    >
    > ![사용자 지정 도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "사용자 지정 도메인 관리")
9. 웹 앱이 만들어지면 아래에 있는 링크를 클릭 합니다 **URL** 열을 새 웹 앱이 실행 중인지 확인 합니다.

    ![새 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *새 웹 앱으로 이동*

    ![웹 앱 실행](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *웹 앱 실행*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>작업 2-프로덕션 SQL 데이터베이스 만들기

이 작업을 사용 하 여 합니다 **Entity Framework Code First 마이그레이션을** 대상으로 하는 데이터베이스를 만들려면 합니다 **Azure SQL Database** 이전 태스크에서 만든 인스턴스.

1. 관리 포털에서 이전 태스크에서 만든 웹 앱으로 이동 하 고 이동할 해당 **대시보드**합니다.
2. 에 **대시보드** 페이지에서 **연결 문자열 보기** 링크를 **눈** 섹션입니다.

    ![연결 문자열 보기](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "연결 문자열 보기")

    *연결 문자열 보기*
3. 복사 합니다 **연결 문자열** 값 및 대화 상자를 닫습니다.

    ![Azure 관리 포털에서 연결 문자열](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 관리 포털에서 연결 문자열")

    *Azure 관리 포털에서 연결 문자열*
4. 클릭 **SQL Database** Azure에서 SQL 데이터베이스의 목록을 보려면

    ![SQL Database 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database 메뉴")

    *SQL Database 메뉴*
5. 이전 태스크에서 만든 데이터베이스를 찾아서 서버를 클릭 합니다.

    ![SQL Database 서버](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database 서버")

    *SQL Database 서버*
6. 에 **빠른 시작** 페이지에서 서버를 클릭 **구성**합니다.

    ![구성 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "구성 메뉴")

    *메뉴를 구성 합니다.*
7. 에 **허용 된 IP 주소** 섹션을 클릭 **허용 되는 IP 주소를 추가할** IP SQL Database 서버에 연결할 수 있도록 링크 합니다.

    ![허용 된 IP 주소](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "허용 된 IP 주소")

    *허용 된 IP 주소*
8. 클릭 **저장할** 단계를 완료 하려면 페이지 맨 아래에 있습니다.
9. Visual Studio로 다시 전환 합니다.
10. 에 **패키지 관리자 콘솔**을 대체 하는 다음 명령을 실행 *[YOUR CONNECTION STRING]* 자리 표시자를 Azure에서 복사한 연결 문자열

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![Windows Azure SQL Database를 대상으로 하는 데이터베이스 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL Database를 대상으로 하는 데이터베이스 업데이트")

    *Azure SQL Database를 대상으로 하는 데이터베이스 업데이트*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>작업 3 – Git를 사용 하 여 스테이징 배포 Geek 퀴즈

이 작업에서는 웹 앱의 스테이징 된 게시를 사용 합니다. 그런 다음 Geek 퀴즈 응용 프로그램 로컬 컴퓨터에서 직접 웹 앱의 스테이징 환경에 게시 하는 Git을 사용 합니다.

1. 포털로 돌아가서 웹 응용 프로그램의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.

    ![웹 앱 관리 페이지 열기](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *웹 앱 관리 페이지 열기*
2. 로 이동 합니다 **확장** 페이지입니다. 아래는 **일반** 섹션에서 **표준** 구성 및 클릭 **저장** 명령 모음에서.

    > [!NOTE]
    > 현재 지역 및 구독에서 모든 웹 앱을 실행 하 **표준** 모드를 두고 합니다 **모두 선택** 확인란을 선택 합니다 **사이트 선택** 구성 합니다. 그렇지 않으면 선택을 취소 합니다 **모두 선택** 확인란 합니다.

    ![웹 앱을 표준 모드로 업그레이드](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "를 표준 모드로 업그레이드 하는 웹 앱")

    *웹 앱을 표준 모드로 업그레이드*
3. 클릭 **예** 변경을 확인 합니다.

    ![표준 모드로 변경 확인](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "웹 앱 모드를 변경 하는 계속")

    *표준 모드로 변경 확인*
4. 로 이동 합니다 **대시보드** 페이지를 클릭 **스테이징 된 게시를 사용 하도록 설정** 아래에서 **간략 상태** 섹션.

    ![스테이징 된 게시를 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "스테이징 된 게시를 사용 하도록 설정")

    *스테이징 된 게시를 사용 하도록 설정*
5. 클릭 **예** 스테이징 된 게시를 사용 하도록 설정 합니다.

    ![스테이징 된 게시를 확인](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "스테이징 된 게시를 사용 하도록 설정 하려면 예 클릭")

    *스테이징 된 게시를 확인합니다.*
6. 웹 앱의 목록에서 스테이징 사이트 슬롯을 표시 하려면 웹 앱 이름 왼쪽에 표시를 확장 합니다. 뒤에 웹 앱의 이름이 ***(준비)*** 합니다. 관리 페이지로 이동 하려면 스테이징 사이트를 클릭 합니다.

    ![스테이징 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "스테이징 웹 앱으로 이동")

    *스테이징 앱으로 이동*
7. 해당 그 관리 페이지가 다른 웹 앱의 관리 페이지와 같은 알 수 있습니다. 로 이동 합니다 **배포** 페이지 및 복사 합니다 **Git URL** 값입니다. 이 연습 뒷부분에서를 사용 합니다.

    ![Git URL 값을 복사합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *Git URL 값을 복사합니다.*
8. 새 **Git Bash** 콘솔 및 다음 명령을 실행 합니다. 업데이트를 *[YOUR 응용 프로그램 경로]* 자리 표시자에 대 한 경로를 합니다 **GeekQuiz** 솔루션에는 **Source\Ex1 DeployingWebSiteToStaging\Begin** 의 폴더 이 실습 합니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 초기화 및 첫 번째 커밋](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git 초기화 및 첫 번째 커밋*
9. 원격 웹 앱을 푸시 하려면 다음 명령을 실행 **Git** 리포지토리. 관리 포털에서 가져온 URL을 사용 하 여 자리 표시자를 대체 합니다. 배포 암호에 대 한 라는 메시지가 표시 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure에 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *Azure에 푸시*

    > [!NOTE]
    > FTP 호스트 또는 웹 앱의 GIT 리포지토리에 콘텐츠를 배포할 때 사용 하 여 인증 해야 합니다 **배포 자격 증명** 웹 앱에서 만든 **퀵스타트** 또는 **대시보드**  관리 페이지입니다. 배포 자격 증명을 알 수 없는 경우 관리 포털을 사용 하 여 쉽게 재설정할 수 있습니다. 웹 앱을 엽니다 **대시보드** 페이지를 클릭 합니다 **배포 자격 증명 재설정** 링크 합니다. 새 암호를 입력 하 고 클릭 **확인**합니다. 배포 자격 증명은 구독과 연결 된 모든 web apps를 사용 하 여 사용 하기에 적합 합니다.
10. Azure에 성공적으로 푸시된 웹 앱을 확인 하기 위해 다시 관리 포털로 이동 하 고 클릭 **Websites**합니다.
11. 웹 앱을 찾아 스테이징 사이트 슬롯을 표시 하려면 항목을 확장 합니다. 클릭 해당 **이름을** 관리 페이지로 이동 합니다.
12. 클릭 **배포** 보려는 합니다 **배포 기록**합니다. 있는지 확인 하십시오는 **활성 배포가** 사용 하 여 프로그램  *&quot;초기 커밋&quot;* 합니다.

    ![활성 배포](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *활성 배포*
13. 마지막으로, 클릭 **찾아보기** 웹 앱으로 이동 하려면 명령 모음에서.

    ![웹 앱 찾아보기](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *웹 앱 찾아보기*
14. 응용 프로그램을 성공적으로 배포한 경우 Geek 퀴즈 로그인 페이지가 표시 됩니다.

    > [!NOTE]
    > 배포 된 응용 프로그램의 주소 URL은 뒤에 웹 앱의 이름을 포함 *-스테이징*합니다.

    ![스테이징 환경에서 실행 중인 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *스테이징 환경에서 실행 중인 응용 프로그램*
15. 응용 프로그램을 탐색 하려는 경우 클릭 **등록** 새 사용자를 등록 합니다. 사용자 이름, 전자 메일 주소 및 암호를 입력 하 여 계정 세부 정보를 완료 합니다. 다음으로, 응용 프로그램에서는 퀴즈의 첫 번째 질문을 보여 줍니다. 이 예상 대로 작동 하는지 확인 하려면 몇 가지 질문에 답변 합니다.

    ![응용 프로그램을 사용할 준비가 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *응용 프로그램을 사용할 준비가 되었습니다.*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>작업 4-프로덕션 웹 앱을 승격 합니다.

웹 앱 스테이징 환경에서 제대로 작동 하는지 확인 했으므로 프로덕션으로 승격할 준비가 되었습니다. 이 태스크에서는 프로덕션 사이트 슬롯을 사용 하 여 스테이징 사이트 슬롯을 교환 됩니다.

1. 관리 포털에 다시 이동 하 고 스테이징 사이트 슬롯을 선택 합니다. 클릭 **교환** 명령 모음에서.

    ![프로덕션으로 교환](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *프로덕션으로 교환*
2. 클릭 **예** 스왑 작업을 계속 하려면 확인 대화 상자에서. Azure가 즉시 스테이징 사이트의 콘텐츠를 사용 하 여 프로덕션 사이트의 콘텐츠를 교환 합니다.

    > [!NOTE]
    > 일부 설정은 준비 된 버전에서 프로덕션 버전 (예: 연결 문자열 재정의 처리기 매핑 등)에 자동으로 복사 됩니다 있지만 (예: DNS 끝점, SSL 바인딩 등)에 다른 설정은 변경 되지 않습니다.

    ![교환 작업 확인](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *교환 작업 확인*
3. 교체가 완료 되 면 프로덕션 슬롯을 선택 하 고 클릭 **찾아보기** 프로덕션 사이트를 열려면 명령 모음에서. 주소 표시줄에 URL을 확인 합니다.

    > [!NOTE]
    > 캐시의 선택을 취소 하려면 브라우저를 새로 고침 해야 합니다. Internet Explorer에서 하면이 키를 눌러 **CTRL + R**합니다.

    ![프로덕션 환경에서 실행 중인 웹 앱](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. 에 **GitBash** 콘솔에서 프로덕션 슬롯을 대상으로 로컬 Git 리포지토리에 대 한 원격 URL을 업데이트 합니다. 이 위해 배포 사용자 이름을 웹 앱의 이름을 사용 하 여 자리 표시자를 대체 하는 다음 명령을 실행 합니다.

    > [!NOTE]
    > 다음 실습에서 랩의 단순성에 대 한 스테이징 대신 프로덕션 사이트에 변경 내용을 푸시할 됩니다. 실제 시나리오에서 프로덕션으로 수준을 올리기 전에 스테이징 환경에서 변경 내용을 확인 하는 것이 좋습니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>연습 3: 프로덕션 환경에서 배포 롤백 수행

시나리오가 없는 없는 스테이징과 프로덕션, 예를 들어 간에 핫 스왑 하는 데 스테이징 슬롯을 사용 하는 경우 **무료** 하거나 **공유** 모드입니다. 이러한 시나리오에서는 테스트 해야 테스트 환경에서 응용 프로그램-로컬 또는 원격 사이트에 – 프로덕션에 배포 하기 전에 합니다. 그러나 가능성이 프로덕션 사이트에서 테스트 단계 중에 검색 되지 문제가 발생할 수는 있습니다. 이 예제의 경우 쉽게 응용 프로그램의 이전 및 더 안정적인 버전으로 가능한 한 빨리 전환 하는 메커니즘을 마련해 야 합니다.

**Azure App Service**, 소스 제어의 연속 배포를 통해이 가능한 감사 인사를 전 합니다 **재배포** 관리 포털에서 사용할 수 있는 작업입니다. Azure 연결 된 리포지토리에 푸시된 커밋과 배포를 추적 하 고 이전 배포를 사용 하 여 언제 든 지 응용 프로그램을 다시 배포 하는 옵션을 제공 합니다.

이 연습에서는 코드에 대 한 변경 수행 합니다 **Geek 퀴즈** 의도적으로 삽입 하는 응용 프로그램을 *버그*합니다. 오류를 확인 하려면 프로덕션 환경에 응용 프로그램 배포 및 다음 있습니다 이용 하는 이전 상태로 다시 이동 하는 재배포 기능.

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>작업 1-Geek 퀴즈 응용 프로그램 업데이트

이 태스크에서는 코드의 작은 조각을 리팩터링 합니다 **TriviaController** 클래스의 새 메서드로 데이터베이스에서 선택한 퀴즈 옵션을 검색 하는 논리 부분을 추출 합니다.

1. 사용 하 여 Visual Studio 인스턴스를 전환 합니다 **GeekQuiz** 이전 연습에서 솔루션입니다.
2. **솔루션 탐색기**오픈를 **TriviaController.cs** 파일을 **컨트롤러** 폴더.
3. 찾을 합니다 **StoreAsync** 메서드와 다음 그림에 강조 표시 된 코드를 선택 합니다.

    ![코드를 선택합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *코드를 선택합니다.*
4. 확장 하 고, 선택한 코드를 마우스 오른쪽 단추로 클릭 합니다 **리팩터링** 선택한 메뉴 **메서드 추출...** .

    ![새 메서드로 코드를 추출합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *Extract 메서드를 선택합니다.*
5. 에 **메서드 추출** 대화 상자에서 새 메서드 이름 *MatchesOption* 클릭 **확인**합니다.

    ![메서드 이름을 지정합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *추출한 메서드에 대 한 이름을 지정합니다.*
6. 선택한 코드를 다음으로 추출 합니다 **MatchesOption** 메서드. 결과 코드는 다음 코드 조각에 표시 됩니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>작업 2-Geek 퀴즈 응용 프로그램을 재배포

이제 프로덕션 환경에 새 배포를 트리거할 리포지토리에 이전 태스크에서 수행한 변경 내용을 푸시할가 있습니다. 사용 하 여 문제를 트러블 슈팅는 그런 다음 합니다 **F12 개발 도구** Internet Explorer에서 제공 하 고 Azure 관리 포털에서 롤백 이전 배포를 수행 합니다.

1. 새 **Git Bash** Azure App Service에 대 한 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.
2. Azure에 변경 내용을 적용 하려면 다음 명령을 실행 합니다. 업데이트를 *[YOUR 응용 프로그램 경로]* 에 대 한 경로 사용 하 여 자리 표시자를 **GeekQuiz** 솔루션입니다. 배포 암호에 대 한 라는 메시지가 표시 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![리팩터링된 코드에서 Azure로 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *리팩터링된 코드에서 Azure로 푸시*
3. Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`). 이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.
4. 키를 눌러 **F12** 개발 도구를 시작 하려면 합니다 **네트워크** 탭을 클릭 합니다 **재생** 기록을 시작 하려면 단추입니다.

    ![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "네트워크 녹음/녹화 시작")

    *네트워크 녹음/녹화 시작*
5. 퀴즈의 옵션을 선택 합니다. 아무 작업도 볼 수 있습니다.
6. 에 **F12** 창에서 POST HTTP 요청에 해당 항목은 HTTP를 보여 줍니다 **500** 결과입니다.

    ![HTTP 500 오류](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 오류*
7. 선택 된 **콘솔** 탭 합니다. 오류 원인의 세부 정보를 사용 하 여 기록 됩니다.

    ![로그인된 오류](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *로그인된 오류*
8. 오류 세부 정보 부분을 찾습니다. 물론이 오류는 이전 단계에서 커밋된 있습니다 리팩터링 코드에서 발생 합니다.

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.
9. 브라우저를 닫지 마세요.
10. 새 브라우저 인스턴스를 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com) 구독과 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.
11. 선택 **Websites** 연습 2에서 만든 웹 앱을 클릭 합니다.
12. 로 이동 합니다 **배포** 페이지입니다. 모든 커밋을 수행 하는 배포 기록에 나열 됩니다.

    ![기존 배포의 목록](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *기존 배포의 목록*
13. 이전 커밋을 선택 하 고 클릭 **재배포** 명령 모음에서.

    ![이전 커밋 재배포](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *이전 커밋 재배포*
14. 확인 대화 상자가 나타나면 클릭 **예**합니다.

    ![재배포를 확인합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. 배포가 완료 되 면 웹 앱 및 키를 눌러 브라우저 인스턴스를 다시 전환 **ctrl+f5**합니다.
16. 옵션 중 하나를 클릭 합니다. 위치 및 결과 플립 애니메이션이 수행 됩니다 (*수정/잘못 된*) 표시 됩니다.
17. (선택 사항) 으로 전환 합니다 **Git Bash** 콘솔 및 이전 커밋으로 되돌리려면 다음 명령을 실행 합니다.

    > [!NOTE]
    > 이러한 명령에 잘못 된 커밋의 Git 리포지토리에 모든 변경 내용을 실행 취소 하는 새 커밋이 만들어집니다. Azure 새 커밋을 사용 하 여 응용 프로그램을 재배포 후 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>실습 4: Azure Storage를 사용 하 여 확장

**Blob** 많은 양의 구조화 되지 않은 텍스트 또는 비디오, 오디오 및 이미지와 같은 이진 데이터를 저장 하는 가장 간단한 방법입니다. 저장소에 응용 프로그램의 정적 콘텐츠를 이동, 브라우저에 직접 이미지 또는 문서를 제공 함으로써 응용 프로그램을 확장할 수 있습니다.

이 연습에서는 Blob 컨테이너에 응용 프로그램의 정적 콘텐츠를 이동 합니다. 추가할 응용 프로그램을 구성 하는 다음을 **ASP.NET URL 재작성 규칙** 에 **Web.config** Blob 컨테이너에 콘텐츠를 리디렉션할 수입니다.

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>작업 1-Azure Storage 계정 만들기

이 작업을 관리 포털을 사용 하 여 새 저장소 계정을 만드는 방법을 배웁니다.

1. 로 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com) 구독과 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.
2. 선택 **새 | Data Services | 저장소 | 빠른 생성** 새 저장소 계정 만들기를 시작 합니다. 선택한 계정에 대 한 고유한 이름을 입력 한 **지역** 목록에서. 클릭 **Storage 계정 만들기** 를 계속 합니다.

    ![새 저장소 계정을 만들](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "새 저장소 계정 만들기")

    *새 저장소 계정 만들기*
3. 에 **저장소** 섹션에서 새 저장소 계정의 상태가으로 변경 될 때까지 기다립니다 *Online* 다음 단계를 진행 하기 위해.

    ![만든 저장소 계정](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "만든 저장소 계정")

    *만든 저장소 계정*
4. 저장소 계정 이름을 클릭 한 다음 클릭 합니다 **대시보드** 페이지의 맨 위에 있는 링크입니다. 합니다 **대시보드** 페이지 계정과 응용 프로그램 내에서 사용할 수 있는 서비스 끝점의 상태에 대 한 정보를 제공 합니다.

    ![저장소 계정 대시보드 표시](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "저장소 계정 대시보드를 표시 합니다.")

    *저장소 계정 대시보드를 표시합니다.*
5. 클릭 합니다 **액세스 키 관리** 탐색 모음에서 단추입니다.

    ![관리 액세스 키 단추](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "액세스 키 관리 단추")

    *관리 액세스 키 단추*
6. 에 **액세스 키 관리** 대화 상자에서 복사를 **저장소 계정 이름** 및 **기본 액세스 키** 다음 예에서는 해당 필요 하므로 합니다. 그런 다음 대화 상자를 닫습니다.

    ![관리 액세스 키 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "액세스 키 관리 대화 상자")

    *관리 액세스 키 대화 상자*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>작업 2-Azure Blob Storage에 자산 업로드

이 태스크에서는 저장소 계정에 연결 하려면 Visual Studio에서 서버 탐색기 창을 사용 합니다. 다음 blob 컨테이너를 만들고 컨테이너에 도전할 퀴즈 로고를 사용 하 여 파일을 업로드 합니다.

1. 사용 하 여 Visual Studio 인스턴스를 전환 합니다 **GeekQuiz** 이전 연습에서 솔루션입니다.
2. 메뉴 모음에서 선택 **뷰** 을 클릭 한 다음 **서버 탐색기**합니다.
3. **서버 탐색기**, 마우스 오른쪽 단추로 클릭 합니다 **Azure** 노드와 선택 **Azure에 연결 하는 중...** . 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.

    ![Windows Azure에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *Azure에 연결*
4. 확장 된 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **저장소** 선택한 **외부 저장소 연결 하는 중...** .
5. 에 **새 저장소 계정 추가** 대화 상자에 입력를 **계정 이름** 및 **계정 키** 고 이전 작업에서 가져온 **확인**.

    ![새 저장소 계정 대화 상자를 추가 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *새 저장소 계정 대화 상자를 추가 합니다.*
6. 저장소 계정 아래에 표시 해야 합니다 **저장소** 노드. 저장소 계정을 확장 하 고 마우스 오른쪽 단추로 클릭 **Blob** 선택한 **Blob 컨테이너 만들기...** .

    ![Blob 컨테이너 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob 컨테이너 만들기")

    *Blob 컨테이너 만들기*
7. 에 **Blob 컨테이너 만들기** 대화 상자, blob 컨테이너에 대 한 이름을 입력 하 고 클릭 **확인**합니다.

    ![Create Blob Container 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob 컨테이너 만들기 대화 상자")

    *Blob 컨테이너 만들기 대화 상자*
8. 새 blob 컨테이너에 추가 해야 합니다 **Blob** 노드. 컨테이너가 공개 되도록 컨테이너에 액세스 권한을 변경 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **이미지** 선택한 컨테이너 **속성**합니다.

    ![컨테이너 속성을 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "컨테이너 속성 이미지")

    *이미지 컨테이너 속성*
9. 에 **속성** 창에서 **공용 읽기 액세스** 에 **컨테이너**합니다.

    ![공용 읽기 액세스 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "공용 읽기 액세스 속성 변경")

    *공용 읽기 액세스 속성 변경*
10. 공용 액세스 속성을 변경 하려는 경우 메시지가 표시 되 면 **예**합니다.

    ![Microsoft Visual Studio 경고](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 경고")

    *Microsoft Visual Studio 경고*
11. **서버 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **이미지** blob 컨테이너 및 선택 **Blob 컨테이너 보기**합니다.

    ![Blob 컨테이너를 볼](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob 컨테이너 보기")

    *Blob 컨테이너 보기*
12. 이미지 컨테이너 새 창에서 열고는 항목이 없으면 범례가 표시 되도록 해야 합니다. 클릭 합니다 **업로드** 아이콘 파일을 blob 컨테이너에 업로드 합니다.

    ![항목이 없는 이미지 컨테이너가](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "항목이 없는 이미지 컨테이너")

    *항목이 없는 이미지 컨테이너*
13. 에 **Blob 업로드** 대화 상자에서 **자산** 랩의 폴더입니다. 선택 된 **로고 big.png** 파일을 클릭 **오픈**합니다.
14. 파일을 업로드할 때까지 기다립니다. 업로드가 완료 되 면 이미지 컨테이너에 파일을 나열 합니다. 파일 항목을 마우스 오른쪽 단추로 누르고 **URL 복사**합니다.

    ![Blob URL을 복사](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "blob 파일 URL 복사")

    *Blob URL 복사*
15. Internet Explorer를 열고 URL을 붙여 넣습니다. 다음 이미지는 브라우저에 표시 되어야 합니다.

    ![Windows Blob Storage에서 이미지 로고 big.png](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "저장소에서 big.png 로고 이미지")

    *Azure Blob Storage에서 big.png 로고 이미지*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>작업 3 – Azure Blob Storage에서 정적 콘텐츠를 사용 하는 솔루션 업데이트

이 태스크에서는 구성 된 **GeekQuiz** 이미지를 사용 하는 솔루션 Azure Blob Storage에 업로드 (대신 웹 앱에 있는 이미지)에서 ASP.NET URL 다시 쓰기 규칙을 추가 하 여는 **web.config**파일입니다.

1. Visual Studio에서 엽니다는 **Web.config** 파일을 **GeekQuiz** 찾아서 프로젝트를 **&lt;system.webServer&gt;** 요소.
2. 저장소 계정 이름을 사용 하 여 자리 표시자를 업데이트는 URL 재작성 규칙을 추가 하려면 다음 코드를 추가 합니다.

    (코드 조각- *WebSitesInProduction-Ex4-UrlRewriteRule*)

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL 재작성은 들어오는 웹 요청을 가로채 고 다른 리소스에 요청을 리디렉션하는 프로세스입니다. URL 재작성 규칙에 요청을 필요로 하는 경우가 이러한 리디렉션되는 재작성 엔진을 알려 줍니다. 재작성 규칙을 두 개의 문자열로 구성 되기: 요청한 URL에서 찾을 패턴 (일반적으로 사용 하 여 정규식)을 하는 경우를 사용 하 여 패턴을 바꿀 문자열을 찾을 수 있습니다. 자세한 내용은 [ASP.NET의 URL 재작성](https://msdn.microsoft.com/library/ms972974.aspx)합니다.
3. 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.
4. 새 **Git Bash** Azure App Service에 대 한 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.
5. Azure에 변경 내용을 적용 하려면 다음 명령을 실행 합니다. 업데이트를 *[YOUR 응용 프로그램 경로]* 에 대 한 경로 사용 하 여 자리 표시자를 **GeekQuiz** 솔루션입니다. 배포 암호에 대 한 라는 메시지가 표시 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure에 배포 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *Azure에 배포 업데이트*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>작업 4-확인

이 작업에서는 사용 하 여 **Internet Explorer** 이동할 합니다 **매니아 퀴즈** 응용 프로그램 및 확인을 URL 재작성 규칙 이미지 작동 하는 사용자가 리디렉션됩니다에서 호스팅되는 이미지가 **Azure Blob 저장소**합니다.

1. Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`). 이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.

    ![이미지를 사용 하 여 Geek 퀴즈 웹 앱을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "이미지로 Geek 퀴즈 웹 앱을 표시")

    *이미지를 사용 하 여 Geek 퀴즈 웹 앱을 표시*
2. 키를 눌러 **F12** 개발 도구를 시작 하려면 선택 합니다 **네트워크** 탭 및 기록을 시작 합니다.

    ![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "네트워크 녹음/녹화 시작")

    *네트워크 녹음/녹화 시작*
3. 키를 눌러 **ctrl+f5** 웹 페이지를 새로 고쳐야 합니다.
4. HTTP 요청에 대 한 페이지 로드가 완료 되 면 표시 합니다 **/img/logo-big.png** HTTP 사용 하 여 URL **301** (리디렉션) 결과 및 다른 요청을 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` HTTP사용하여URL**200** 결과입니다.

    ![확인 URL 리디렉션](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "리디렉션 개발 도구에 표시")

    *URL 리디렉션 확인*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>실습 5: 웹 앱에 대 한 자동 크기 조정 사용

> [!NOTE]
> 웹 부하에 대 한 지원이 필요 하므로이 실습은 선택 사항 &amp; 에서만 사용할 수 있는 성능 테스트 **Visual Studio 2013 Ultimate Edition**합니다. Visual Studio 2013의 특정 기능에 대 한 자세한 내용은 버전 비교 [여기](https://www.microsoft.com/visualstudio/eng/products/compare)합니다.


**Azure App Service Web Apps** 에서 실행 중인 웹 앱에 대 한 자동 크기 조정 기능을 제공 **표준 모드**합니다. 자동 크기 조정에 Azure를 부하에 따라 웹 앱의 인스턴스 수를 자동으로 확장할 수 있습니다. 자동 크기 조정 설정 되 면 Azure 웹 앱의 CPU가 5 분 마다 한 번 확인 하 고 해당 시점에 필요한 만큼 인스턴스가 추가 합니다. CPU 사용량이 낮은 경우 인스턴스가 제거 됩니다 두 시간 마다 한 번씩 웹 앱의 성능을 성능이 저하 되었음을 확인 합니다.

이 연습에서 구성 하는 데 필요한 단계를 통해 이동 합니다 **자동 크기 조정** 에 대 한 기능을 **Geek 퀴즈** 웹 앱입니다. 인스턴스를 업그레이드 하는 트리거를 응용 프로그램에서 충분 한 CPU 부하를 생성 하는 Visual Studio 부하 테스트를 실행 하 여이 기능을 확인 합니다.

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>작업 1-CPU 메트릭을 기반으로 구성 자동 크기 조정

이 태스크에서는 연습 2에서 만든 웹 앱에 대 한 자동 크기 조정 기능을 사용 하려면 Azure 관리 포털을 사용 합니다.

1. 에 [Azure 관리 포털](https://manage.windowsazure.com/)를 선택 **웹 사이트** 연습 2에서 만든 웹 앱을 클릭 합니다.
2. 로 이동 합니다 **확장** 페이지입니다. 아래는 **용량** 섹션에서 **CPU** 에 대 한 합니다 **메트릭 별 크기 조정** 구성 합니다.

    > [!NOTE]
    > CPU 별 크기 조정 하는 경우 Azure CPU 사용량을 변경 하는 경우 앱을 사용 하는 인스턴스 수를 동적으로 조정 합니다.

    ![CPU 별 크기 조정 하도록 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "자동 크기 조정에 대 한 CPU 메트릭 선택")

    *CPU 별 크기 조정 하도록 선택*
3. 변경 된 **대상 CPU** 구성을 **20**-**40** 백분율입니다.

    > [!NOTE]
    > 이 범위는 웹 앱에 대 한 평균 CPU 사용량을 나타냅니다. Azure을 추가 하거나이 범위에서 웹 앱을 유지 하도록 인스턴스를 제거 합니다. 에 지정 된 크기 조정 시 사용 되는 인스턴스의 최소 및 최대 수를 **인스턴스 수** 구성 합니다. Azure 위나 제한을 벗어나서 이동 하지 않습니다.
    >
    > 기본값 **대상 CPU** 값은이 랩의 목적에 대해서만 수정 합니다. 작은 값을 사용 하 여 CPU 범위를 구성 하 여 보통 수준의 부하는 응용 프로그램에 배치 되 면 자동 크기 조정 트리거와 가능성은 증가 합니다.

    ![변경 대상 CPU 20%에서 40% 사이 여야](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "20%에서 40% 사이 여야 CPU 대상 변경")

    *변경 대상 CPU 20%에서 40% 사이 여야*
4. 클릭 **저장할** 변경 내용을 저장 하려면 명령 모음에서 합니다.

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>작업 2-부하 테스트를 Visual Studio를 사용 하 여

이제 **자동 크기 조정** 되었습니다 구성 만듭니다는 **웹 성능 및 부하 테스트 프로젝트** 웹 앱에서 일부 CPU 부하를 생성 하는 Visual Studio에서.

1. 오픈 **Visual Studio Ultimate 2013** 선택한 **파일 | 새 | 프로젝트...**  새 솔루션을 시작 합니다.

    ![새 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
2. 에 **새 프로젝트** 대화 상자에서 **웹 성능 및 부하 테스트 프로젝트** 아래에서 **Visual C# | 테스트** 탭 합니다. 했는지 **.NET Framework 4.5** 는 프로젝트의 이름을 선택 *WebAndLoadTestProject*, 선택는 **위치** 클릭 **확인**.

    ![새 웹 및 부하 테스트 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "새 웹 및 부하 테스트 프로젝트 만들기")

    *새 웹 및 부하 테스트 프로젝트 만들기*
3. 에 **WebTest1.webtest** 마우스 오른쪽 단추로 클릭 합니다 **WebTest1** 노드와 클릭 **요청 추가**.

    ![요청 WebTest1 추가할](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "WebTest1 요청 추가")

    *WebTest1 요청 추가*
4. 에 **속성** 창 새 요청 노드의 업데이트는 **Url** 웹 앱의 URL을 가리키도록 속성 (예: *[ http://geek-quiz.azurewebsites.net/ ](http://geek-quiz.azurewebsites.net/)*).

    ![Url 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url 속성 변경")

    *Url 속성 변경*
5. 에 **WebTest1.webtest** 창에서 마우스 오른쪽 단추로 클릭 **WebTest1** 클릭 하 고 **루프 추가...** .

    ![WebTest1에 루프 추가](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "WebTest1에 루프 추가")

    *WebTest1에 루프 추가*
6. 에 **루프에 조건부 규칙 추가 및 항목** 대화 상자에서를 **For 루프** 규칙 및 다음 속성을 수정 합니다.

   1. **종료 값:** 1000
   2. **컨텍스트 매개 변수 이름:** 반복기
   3. **증가값:** 1

      ![루프에 대 한 규칙을 선택 하 고 속성을 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "루프에 대 한 규칙을 선택 하 고 속성 업데이트")

      *루프에 대 한 규칙을 선택 하 고 속성 업데이트*
7. 아래는 **루프의 항목** 섹션 루프에 대 한 첫 번째 및 마지막 항목이 이전에 만든 요청을 선택 합니다. 계속하려면 **확인** 을 클릭합니다.

    ![루프에 대 한 첫 번째 및 마지막 항목 선택](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "루프에 대 한 첫 번째 및 마지막 항목 선택")

    *루프에 대 한 첫 번째 및 마지막 항목 선택*
8. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **WebAndLoadTestProject** 프로젝트를 확장 하 고는 **추가** 메뉴를 선택 **부하 테스트...** .

    ![부하 테스트 프로젝트에 추가 WebAndLoadTestProject](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject 프로젝트에 부하 테스트 추가")

    *부하 테스트 프로젝트에 추가 WebAndLoadTestProject*
9. 에 **부하 테스트 새로 만들기 마법사** 대화 상자, 클릭 **다음**합니다.

    ![부하 테스트 새로 만들기 마법사](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "부하 테스트 새로 만들기 마법사")

    *부하 테스트 새로 만들기 마법사*
10. 에 **시나리오** 페이지에서 **인지 시간을 사용 하지 마십시오** 클릭 **다음**합니다.

    ![선택 하면 대기 시간을 사용할 수 없습니다](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "를 인지 시간을 사용 하지 않도록 선택 하면")

    *인지 시간을 사용 하 여 선택 하지 않음*
11. 에 **부하 패턴** 페이지에서 확인 합니다 **일정 부하** 옵션을 선택 합니다. 변경 합니다 **사용자 수** 설정을 **250** 사용자 및 클릭 **다음**합니다.

    ![사용자 수가 250으로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "250 사용자 수를 변경 합니다.")

    *사용자 수가 250으로 변경*
12. 에 **테스트 조합 모델** 페이지에서 **순차적 테스트 순서 기반** 클릭 **다음**합니다.

    ![테스트 조합 모델 선택](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "테스트 조합 모델 선택")

    *테스트 조합 모델 선택*
13. 에 **테스트 조합 모델** 페이지에서 **추가...**  조합에 테스트를 추가 합니다.

    ![테스트 조합에 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "테스트 조합에 테스트 추가")

    *테스트 조합에 테스트 추가*
14. 에 **테스트 추가** 대화 상자에서 두 번 클릭 **WebTest1** 테스트를 추가 합니다 **선택한 테스트** 목록입니다. 계속하려면 **확인** 을 클릭합니다.

    ![WebTest1 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "WebTest1 테스트 추가")

    *WebTest1 테스트 추가*
15. 다시 합니다 **테스트 조합** 페이지에서 클릭 **다음**합니다.

    ![완료 테스트 조합 페이지](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "완료 테스트 조합 페이지")

    *완료 테스트 조합 페이지*
16. 에 **네트워크 조합** 페이지에서 클릭 **다음**합니다.

    ![네트워크 조합 페이지에서 다음을 클릭 하면](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "네트워크 조합 페이지에서 다음을 클릭 하면")

    *네트워크 조합 페이지에서 다음을 클릭*
17. 에 **브라우저 조합** 페이지에서 **Internet Explorer 10.0** 브라우저 종류와 클릭 **다음**합니다.

    ![브라우저 종류를 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "브라우저 종류를 선택 합니다.")

    *브라우저 종류를 선택합니다.*
18. 에 **카운터 집합** 페이지에서 클릭 **다음**합니다.

    ![카운터 집합 페이지에서 다음을 클릭](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "카운터 집합 페이지에서 다음 클릭")

    *카운터 집합 페이지에서 다음을 클릭합니다.*
19. 에 **실행 설정** 페이지에서 설정 합니다 **부하 테스트 지속 시간** 를 **5 분** 클릭 **완료**.

    ![부하 테스트 지속 시간을 5 분으로 설정](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "부하 테스트 지속 시간을 5 분으로 설정")

    *부하 테스트 지속 시간을 5 분으로 설정*
20. **솔루션 탐색기**를 두 번 클릭 합니다 **Local.settings** 테스트 설정을 탐색 하는 파일입니다. 기본적으로 Visual Studio는 테스트를 실행 하려면 로컬 컴퓨터를 사용 합니다.

    > [!NOTE]
    > 또는 사용 하 여 클라우드 부하 테스트를 실행 하려면 테스트 프로젝트를 구성할 수 있습니다 **Azure 테스트 계획**합니다. 테스트 계획을 azure 클라우드 기반 부하 테스트를 좀 더 현실적인 로드를 시뮬레이션 하는 서비스, CPU 용량, 사용 가능한 메모리 및 네트워크 대역폭과 같은 로컬 환경 제약 조건을 방지를 제공 합니다. Azure 테스트 계획을 사용 하 여 부하 테스트를 실행 하는 방법에 대 한 자세한 내용은 참조 하십시오 [부하 테스트 시나리오](/azure/devops/test/load-test/overview?view=vsts)합니다.

    ![테스트 설정](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>작업 3 – 자동 크기 조정 확인

이제 이전 태스크에서 만든 부하 테스트를 실행 하 고 웹 앱 부하 상태에서 어떻게 동작 하는지 확인 됩니다.

1. **솔루션 탐색기**를 두 번 클릭 **LoadTest1.loadtest** 를 부하 테스트를 엽니다.

    ![LoadTest1.loadtest 열기](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "LoadTest1.loadtest 열기")

    *열기 LoadTest1.loadtest*
2. 에 **LoadTest1.loadtest** 창에서 부하 테스트를 실행 하려면 도구 상자에서 첫 번째 단추를 클릭 합니다.

    ![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "부하 테스트 실행")

    *부하 테스트 실행*
3. 부하 테스트가 완료 될 때까지 기다립니다.

    > [!NOTE]
    > 부하 테스트는 동시에 웹 앱에 요청을 전송 하는 여러 사용자를 시뮬레이션 합니다. 테스트를 실행 하는 경우에 모든 오류, 경고 또는 부하 테스트 실행에 관련 된 기타 정보를 검색 하려면 사용 가능한 카운터를 모니터링할 수 있습니다.

    ![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "부하 테스트가 완료 될 때까지 대기")

    *부하 테스트 실행*
4. 테스트가 완료 되 면 관리 포털로 돌아가서로 이동 합니다 **확장** 웹 앱의 페이지입니다. 아래는 **용량** 섹션인 표시 그래프의 새 인스턴스를 자동으로 배포 되었습니다.

    ![새 인스턴스를 자동으로 배포](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *새 인스턴스를 자동으로 배포*

    > [!NOTE]
    > 변경 내용을 그래프에 표시 하려면 몇 분 정도 걸릴 수 있습니다 (키를 눌러 **ctrl+f5** 주기적으로 페이지를 새로). 모든 변경 내용이 표시 되지 않으면, 다음을 시도할 수 있습니다.
    >
    > - 부하 테스트 시간을 증가 시킬 (예: **10 분**)
    > - 최대값과 최소값을 줄일 합니다 **대상 CPU** 웹 앱의 자동 크기 조정 구성의 범위
    > - 사용 하 여 클라우드에서 부하 테스트 실행 **Azure 테스트 계획**합니다. 자세한 내용은 [여기](/azure/devops/test/load-test/index?view=vsts)

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습에서는 설정 하 고 응용 프로그램 Azure에서 프로덕션 웹 앱을 배포 하는 방법을 알아보았습니다. 검색 하 고 사용 하 여 데이터베이스를 업데이트 하 여 시작 **Entity Framework Code First 마이그레이션을**를 사용 하 여 사이트의 새 버전을 배포 하 여 계속 **Git** 롤백 수행 하는 안정적인 최신 버전의 사이트입니다. 또한 Blob 컨테이너에 정적 콘텐츠를 이동 하려면 저장소를 사용 하 여 앱의 크기를 조정 하는 방법을 알아보았습니다.
