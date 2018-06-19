---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드 | Microsoft Docs
author: microsoft
description: 3 단계는 म 두 쿼리를 사용 하 고 업데이트할 수 데이터베이스 업그레이드 되었으며 수정 응용 프로그램에 대 한 모델을 만드는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: c5a482474fd2f41836f70952306ada5cd9136455
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874943"
---
<a name="build-a-model-with-business-rule-validations"></a>비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 3 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 3 단계는 म 두 쿼리를 사용 하 고 업데이트할 수 데이터베이스 업그레이드 되었으며 수정 응용 프로그램에 대 한 모델을 만드는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-3-building-the-model"></a>업그레이드 되었으며 수정 단계 3: 모델을 구축

모델-뷰-컨트롤러 프레임 워크에서 "모델" 용어 된 유효성 검사 및 비즈니스 규칙을 통합 하는 해당 도메인 논리는 응용 프로그램의 데이터를 나타내는 개체를 나타냅니다. MVC 기반 응용 프로그램의 여러 가지 "핵심" 점에서 모델과 근본적으로 나중에 볼 수 있겠지만 드라이브의 동작입니다.

ASP.NET MVC 프레임 워크를 지 원하는 모든 데이터 액세스 기술을 사용 하 고 개발자는 다양 한 포함 하 여 해당 모델을 구현 하는 풍부한.NET 데이터 옵션 중에서 선택할 수 있습니다: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, subsonic은 이러한 방식을, WilsonORM, 또는 원시 ADO. NET DataReaders 또는 데이터 집합입니다.

업그레이드 되었으며 수정 응용 프로그램에 대 한을 하겠습니다 우리의 데이터베이스 디자인에 매우 밀접 하 게 해당 하 고 일부 사용자 지정 유효성 검사 논리와 비즈니스 규칙을 추가 하는 간단한 모델을 만들려면 LINQ to SQL 사용 합니다. 추상 자리를 비울 도움이 되는 저장소 클래스 구현 다음 합니다 응용 프로그램 및 테스트 쉽게 단위를 사용 하 여 나머지 데이터 지 속성 구현 합니다.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL은.NET 3.5의 일부로 제공 되는 ORM (개체 관계형 매퍼).

LINQ to SQL 쉽게.NET 클래스에 대 한 코드를 작성할 수 있습니다에 데이터베이스 테이블을 매핑할 수 있는 방법을 제공 합니다. 업그레이드 되었으며 수정 응용 프로그램에 대 한 때 사용 해야 Dinners 및 RSVP 테이블 Dinner 및 RSVP 클래스에는 데이터베이스 내에서 매핑할 수 있습니다. Dinners 및 RSVP 테이블의 열 Dinner 및 RSVP 클래스에서 속성에 해당 됩니다. 각 Dinner 및 RSVP 개체는 데이터베이스의 Dinners 또는 RSVP 테이블 내에서 별도 행을 나타냅니다.

LINQ to SQL SQL 문을 검색 하 고 Dinner 및 RSVP 업데이트를 수동으로 생성할 필요가 없도록 하는 데 사용할 수 있으며 데이터베이스 데이터를 사용 하 여 개체입니다. 대신, 매핑되는 방식을/데이터베이스 및 이들 간의 관계에서 Dinner 및 RSVP 클래스를 정의 합니다. LINQ to SQL은 상호 작용 하 고 사용 하는 경우 런타임에 사용할 적절 한 SQL 실행 논리를 생성 한 주의 ´ ù.

VB 및 C#에서 LINQ 언어 지원 Dinner 및 RSVP를 검색 하는 표현 쿼리 작성에 사용할 수는 데이터베이스에서 개체입니다. 이 최소화 되는 데이터는 코드를 작성 하려면 정리 실제로 응용 프로그램을 빌드할 수 있도록 하 고 있습니다.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>이 프로젝트에 LINQ to SQL 클래스 추가

이 프로젝트 내에서 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 알아보고 선택 하겠습니다는 **추가-&gt;새 항목** 메뉴 명령:

![](build-a-model-with-business-rule-validations/_static/image1.png)

이 "새 항목 추가" 대화 상자를 표시 합니다. "데이터" 범주별으로 필터링 알아보고 내에서 "SQL 클래스를 LINQ" 템플릿을 선택 하겠습니다.

![](build-a-model-with-business-rule-validations/_static/image2.png)

"업그레이드 되었으며 수정" 항목 이름을 알아보고 "추가" 단추를 클릭 하겠습니다. Visual Studio 우리의 \Models 디렉터리는 NerdDinner.dbml 파일이 추가 되 고 LINQ to SQL 개체 관계형 디자이너를 엽니다.

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>Linq to SQL 데이터 모델 클래스 만들기

LINQ to SQL 사용 하면 기존 데이터베이스 스키마에서 데이터 모델 클래스를 빠르게 만들 수 있습니다. 할 일에 모델링 하려는이 म 합니다 업그레이드 되었으며 수정 데이터베이스 서버 탐색기에서 열고 테이블 선택:

![](build-a-model-with-business-rule-validations/_static/image4.png)

테이블 LINQ로 SQL 디자이너 화면 끌어 놓을 수 있습니다. 이 LINQ to SQL 수행 하는 경우 Dinner 자동으로 만들어집니다 (데이터베이스 테이블 열에 매핑되는 클래스 속성)을 가진 테이블의 스키마를 사용 하 여 RSVP 클래스 및:

![](build-a-model-with-business-rule-validations/_static/image5.png)

LINQ to SQL 기본적으로 디자이너 자동으로 "복수로 바꿀지" 테이블 및 열 이름을 데이터베이스 스키마를 기반으로 클래스를 만듭니다. 예: 위의 예에는 "Dinners" 테이블 "Dinner" 클래스에서 발생 했습니다. 이와 같은 클래스 이름을 통해 우리의 모델은.NET 명명 규칙과 일치 하 게 일반적으로 해당 디자이너의 수정이 반영 행이 있으면를 편리 하 게 특히 추가할 때 테이블의 많은 찾기. 마음에 들지 않으면 클래스 또는 디자이너 생성 하지만 항상 재정의 하 고 원하는 이름으로 변경할 수 있는 속성의 이름입니다. 이렇게 하려면 두 줄을 편집 하는 엔터티/속성 이름에-디자이너 내에서 하거나 속성 표를 통해 수정 하 여 합니다.

LINQ to SQL 디자이너도 테이블의 기본 키/외래 키 관계를 검사 하 고 자동으로 그에 따라 기본적으로 기본을 만들므로 다른 모델 클래스 간에 "관계 연결" 만듭니다. RSVP 테이블 Dinners 테이블에 외래 키가 있다는 사실에 기반으로 때 우리는 Dinners 끌어서 RSVP 둘 사이 일 대 다 관계 연결을 LINQ to SQL 디자이너에 테이블 유추 된 예를 들어 (이에 화살표로 표시 됩니다는 디자이너):

![](build-a-model-with-business-rule-validations/_static/image6.png)

위의 연결 RSVP 클래스 개발자가 관련 된 주어진된 RSVP 저녁에 액세스 하는 데 사용할 수 있는 강력한 형식의 "Dinner" 속성을 추가 하려면 SQL LINQ 중단 됩니다. 개발자가 검색 하 고 특정 Dinner와 연결 된 RSVP 개체를 업데이트할 수 있는 "RSVPs" 컬렉션 속성이 있어야 Dinner 클래스도 발생 합니다.

다음 새 RSVP 개체를 만든 하는 Dinner 않으십니까 컬렉션에 추가 하는 경우 Visual Studio 내에서 intellisense의 예를 볼 수 있습니다. LINQ to SQL 자동으로 추가 하는 방법과 "않으십니까" 컬렉션 Dinner 개체에서 확인 합니다.

![](build-a-model-with-business-rule-validations/_static/image7.png)

RSVP 개체는 저녁 않으십니까 컬렉션에 추가 하 여 LINQ to SQL Dinner와 데이터베이스에 RSVP 행 간의 외래 키 관계를 연결할 한다는 म:

![](build-a-model-with-business-rule-validations/_static/image8.png)

어떻게 디자이너 모델링 했거나이 테이블 연결을 명명 된, 마음에 들지 않는 경우에이 재정의할 수 있습니다. 디자이너 내에서 연결 화살표를 클릭 하 고 이름 바꾸기, 삭제 또는 수정 하려면 속성 표를 통해 해당 속성에 액세스 합니다. 이 업그레이드 되었으며 수정 응용 프로그램에 대 한 기본 연결 규칙을 작성 하는 데이터 모델 클래스에 대해 잘 작동 하지만 및 방금 기본 동작을 사용할 수 있습니다.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext 클래스

Visual Studio의 모델 및 LINQ to SQL 디자이너를 사용 하 여 정의 하는 데이터베이스 관계를 나타내는.NET 클래스를 자동으로 만들어집니다. 각 LINQ to SQL 디자이너 파일 솔루션에 추가 대 한 LINQ to SQL DataContext 클래스도 생성 됩니다. 우리의 LINQ to SQL 클래스 항목 "업그레이드 되었으며 수정" 이라는 것 때문에 생성 된 DataContext 클래스 "NerdDinnerDataContext"가 호출 됩니다. 이 NerdDinnerDataContext 클래스는 것이 데이터베이스와 상호 작용 하는 기본 방법입니다.

NerdDinnerDataContext 클래스는 두 개의 속성-데이터베이스 내에서 모델링에서는 두 개의 테이블을 나타내는 "RSVPs-" 및 "Dinners"를 표시 합니다. 사용 하 여 C# 데이터베이스에서 쿼리 및 검색 하 고 Dinner 및 RSVP 개체에 해당 속성에 대 한 LINQ 쿼리를 작성 합니다.

다음 코드 NerdDinnerDataContext 개체 인스턴스화를 나중에 발생 하는 Dinners의 시퀀스를 얻기 위해에 대해 LINQ 쿼리를 수행 하는 방법을 보여 줍니다. LINQ 쿼리를 작성할 때 visual Studio는 전체 intellisense를 제공 하 고 여기에서 반환 된 개체 강력한 형식의 하며 intellisense 지원:

![](build-a-model-with-business-rule-validations/_static/image9.png)

허락해 Dinner 및 RSVP 개체를 쿼리 하는 것 외에도 NerdDinnerDataContext도 자동으로 변경에서는 이후에를 통해 검색 하는 Dinner 및 RSVP 개체를 추적 합니다. 데이터베이스에 다시-명시적 SQL 업데이트 코드를 작성할 필요 없이 변경 내용을 쉽게 저장할이 기능을 사용할 수 있습니다.

예를 들어 아래 코드에는 데이터베이스에서 단일 Dinner 개체를 검색, 저녁 속성 중 두 업데이트 및 다음 변경 내용을 데이터베이스에 다시 저장 하는 LINQ 쿼리를 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

위의 코드에 NerdDinnerDataContext 개체는 자동으로 Dinner 개체에서 검색 하는 것에 대 한 속성 변경 내용을 추적 합니다. "SubmitChanges()" 메서드를 호출 하는 경우에 업데이트 된 값을 유지 하려면 데이터베이스에 적절 한 SQL "업데이트" 문을 실행 합니다 것입니다.

### <a name="creating-a-dinnerrepository-class"></a>DinnerRepository 클래스 만들기

작은 응용 프로그램에 대 한 하는 것은 때로는 컨트롤러 LINQ to SQL DataContext 클래스에 대해 직접 작업 하 고 컨트롤러 내에서 LINQ 쿼리를 포함 합니다. 그러나 응용 프로그램은 더 큰 있게,이 방법은 유지 관리 및 테스트 하는 경우 다루기 집니다. 여러 위치에서 동일한 LINQ 쿼리를 복제 합니다. 저희에 게 될 수도 있습니다.

응용 프로그램 유지 관리 및 테스트를 쉽게 만들 수 있는 한 가지 방법은 "repository" 패턴을 사용 하는 것입니다. 저장소 클래스는 데이터 쿼리 및 지 속성 논리와 떨어져 요약이 응용 프로그램에서 데이터 지 속성의 구현 정보를 캡슐화 하는 데 도움이 됩니다. 응용 프로그램 코드를 청소 하는 것 외에도 리포지토리 패턴을 사용 하 여 쉽게 만들 수를 데이터 저장소 구현을 나중에 변경 하 고 실제 데이터베이스를 요구 하지 않고 응용 프로그램을 테스트 하는 단위를 용이 하 게 할 수 있습니다.

업그레이드 되었으며 수정 응용 프로그램에 대 한 사용 하 여 DinnerRepository 클래스 정의 하겠습니다는 아래 서명:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*참고:이 장의이 클래스 로부터 IDinnerRepository 인터페이스 추출 알아보고 하겠습니다 우리의 컨트롤러에 함께 종속성 주입을 사용 하도록 설정 합니다. 로 시작 하지만 하겠습니다 단순 시작한 DinnerRepository 클래스와 직접 작동 합니다.*

이 클래스는 "Models" 폴더를 마우스 오른쪽 단추로 클릭 알아보고 선택 하겠습니다를 구현 하는 **추가-&gt;새 항목** 메뉴 명령입니다. "새 항목 추가" 대화 상자 내에서 "클래스" 템플릿을 선택 하 고 "DinnerRepository.cs" 파일 이름을 합니다.

![](build-a-model-with-business-rule-validations/_static/image10.png)

아래 코드를 사용 하 여 DinnerRespository 클래스를 구현할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>검색, 업데이트, 삽입 및 DinnerRepository 클래스를 사용 하 여 삭제

DinnerRepository 클래스를 만든 했으므로 일반적인 작업에 수행할 수 있는 것을 보여 주는 몇 가지 코드 예제에서 살펴보겠습니다.

#### <a name="querying-examples"></a>예제 쿼리

아래 코드 DinnerID 값을 사용 하 여 단일 Dinner를 검색 합니다.


[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

아래 코드에 대해 모든 향후 dinners 및 루프를 검색합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>삽입 및 업데이트 예제

아래 코드는 두 개의 새 dinners 추가 보여줍니다. 저장소에 추가/수정 사항에 "save" () 메서드를 호출할 때까지 데이터베이스에 커밋되지 않습니다. LINQ to SQL 자동 줄 바꿈되어 모든 변경 내용을 데이터베이스 트랜잭션에서 – 모든 변경이 발생 하거나 리포지토리의 저장할 때 수행 하는 사람은 하거나:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

아래 코드는 기존 Dinner 개체를 검색 하 고에 두 개의 속성을 수정 합니다. 이 저장소에서 "save" () 메서드를 호출할 때 변경이 다시 데이터베이스에 커밋된:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

아래 코드는 저녁을 검색 하 고는 RSVP를 추가 합니다. LINQ to SQL 만들어집니다 (있기 때문에 기본 키/외래 키 관계를 데이터베이스에서 둘 간의) 하는 Dinner 개체에서 않으십니까 컬렉션을 사용 하 여이 없습니다. 이 변경 내용은 저장소에서 "save" () 메서드를 호출할 때 다시 데이터베이스에 새 RSVP 테이블 행으로 유지 됩니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>삭제 예제

아래 코드는 기존 Dinner 개체를 검색 한 다음 삭제를 표시 합니다. 저장소에서 "save" () 메서드를 호출할 때 주 복제본 데이터베이스에 다시 삭제를 커밋합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>유효성 검사 및 비즈니스 규칙 논리 모델 클래스를과 통합

유효성 검사 및 비즈니스 규칙은 데이터를 사용 하는 모든 응용 프로그램의 핵심이 라 할 논리를 통합 합니다.

#### <a name="schema-validation"></a>스키마 유효성 검사

LINQ to SQL 디자이너를 사용 하 여 모델 클래스 정의 되 면 데이터 모델 클래스에서 속성의 데이터 형식이 데이터베이스 테이블의 데이터 형식에 해당 합니다. 예: "datetime" Dinners 테이블에 있는 "EventDate" 열을 사용 하는 경우 LINQ to SQL에서 만든 데이터 모델 클래스 (즉, 기본 제공.NET 데이터 형식)는 "DateTime" 형식의 됩니다. 즉, 여기에 코드에서 정수 또는 부울 값을 할당 하려고 하면 런타임 시에 유효 하지 않은 문자열 형식을 암시적으로 변환 하려고 하면 오류가 자동으로 발생 합니다 경우 컴파일 오류가 발생 합니다.

사용자를 보호 SQL 삽입 공격을 사용할 문자열-를 사용 하는 경우 있습니다 LINQ to SQL 사용 하면 이스케이프 SQL 값도 자동으로 처리 됩니다.

#### <a name="validation-and-business-rule-logic"></a>유효성 검사 및 비즈니스 규칙 논리

스키마 유효성 검사는 첫 번째 단계로, 유용 하지만 거의 충분 합니다. 대부분의 실제 시나리오 여러 속성에 걸쳐, 코드를 실행 하 고 모델의 상태에 대 한 인식을 경우가 수 있는 다양 한 유효성 검사 논리를 지정 하는 기능이 필요 (예: 것 만들어집니다/업데이트/삭제 되거나 도메인별 상태 내에서 마찬가지로 "보관"). 다양 한 다양 한 패턴 및 정의 하 고 모델 클래스에 유효성 검사 규칙을 적용 하는 데 사용할 수 있는 프레임 워크 되며 여러.NET 기반 프레임 워크 하셨습니까 이러한에 도움이 되는 데 사용할 수 있는 합니다. ASP.NET MVC 응용 프로그램 내에서 거의 모든를 사용할 수 있습니다.

업그레이드 되었으며 수정 응용 프로그램을 위해 사용 합니다는 비교적 간단 하 고 직관적인 패턴 우리의 Dinner 모델 개체에는 IsValid 속성과 GetRuleViolations() 메서드 공개 위치 지정 했습니다. IsValid 속성은 true 또는 false 유효성 검사 및 비즈니스 규칙은 모두 유효 여부에 따라 반환 됩니다. GetRuleViolations() 메서드 목록이 규칙 오류를 반환 합니다.

프로젝트 진행에 "partial 클래스"를 추가 하 여 IsValid 및 GetRuleViolations() 예제의 Dinner 모델에 대 한 구현 합니다. Partial 클래스 메서드/속성/이벤트 (예: LINQ to SQL 디자이너에 의해 생성 된 Dinner 클래스) VS 디자이너에서 유지 관리 하는 클래스를 추가 하려면 사용할 수 있으며에서 도구를 코드로 작업 하는 것을 방지 합니다. म \Models 폴더를 마우스 오른쪽 단추로 클릭 하 여이 프로젝트에 새 partial 클래스를 추가할 수 있으며 "새 항목 추가" 메뉴 명령을 선택 합니다. "새 항목 추가" 대화 상자 내에서 "클래스" 템플릿을 선택 하 고 Dinner.cs 이름을 다음 했습니다.

![](build-a-model-with-business-rule-validations/_static/image11.png)

"추가" 단추를 클릭 하면이 프로젝트에 Dinner.cs 파일을 추가 하 고 IDE 내에서 엽니다. 사용 하 여 기본 규칙/유효성 검사 적용 프레임 워크를 구현할 수 있습니다는 아래 코드:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

위의 코드에 대 한 참고 사항:

- 저녁 클래스 앞 키워드로 "부분" – 즉, 그 안에 포함 된 코드는 LINQ to SQL 디자이너에서 생성/유지 하는 클래스와 결합 되며 하나의 클래스로 컴파일됩니다.
- RuleViolation 클래스가 통해 규칙 위반에 대 한 자세한 정보를 제공 하는 프로젝트에 추가 하는 도우미 클래스가입니다.
- Dinner.GetRuleViolations() 메서드를 유효성 검사 및 비즈니스 규칙 평가를 사용 하면 (구현에 곧). 그런 다음 반환 다시는 RuleViolation는 개체 시퀀스의 모든 규칙 오류에 대 한 자세한 정보를 제공 합니다.
- Dinner.IsValid 속성 Dinner 개체 모든 활성 RuleViolations에 있는지 여부를 나타내는 편리한 도우미 속성을 제공 합니다. 저녁 개체를 사용 하 여 언제 든 지 개발자가 적극적으로 확인할 수 있습니다 (하 고 예외가 발생 하지 않습니다).
- Dinner.OnValidate() 부분 메서드를 Dinner 개체를 데이터베이스 내에서 유지 하려고 합니다. 언제 든 지 알림을 받을 수 있는 LINQ to SQL에서 제공 하는 후크 됩니다. 위의 OnValidate() 구현 사용 하면 Dinner에 없는 RuleViolations 저장 하기 전에. 잘못 된 상태에 있으면 LINQ to SQL 트랜잭션을 중단 하 고에 발생할 수 있는 예외가 발생 합니다.

이 방법은 유효성 검사 및 비즈니스 규칙에 통합할 수 있습니다 하는 간단한 프레임 워크를 제공 합니다. 지금은 추가해보겠습니다는 아래 우리의 GetRuleViolations() 메서드에 규칙:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

C#의 "return을 yield" 기능 모든 RuleViolations의 시퀀스를 반환 하를 사용 합니다. 위의 첫 번째 6 개의 규칙 검사는 단순히 null 또는 빈 문자열 속성 우리의 저녁에 일 수 없습니다 적용 합니다. 마지막 규칙 약간 더 흥미롭습니다 이며 호출을 추가할 수 있습니다 되었는지 확인 하는 프로젝트에는 ContactPhone PhoneValidator.IsValidNumber() 도우미 메서드 형식 일치 Dinner의 국가 번호.

사용할 수 있습니다. 이 전화 유효성 검사 지원을 구현 하기 NET의 정규식 지원 합니다. 다음은 추가할 수 있는 간단한 PhoneValidator 구현을 국가별 Regex 패턴 검사를 추가할 수 있도록 하는 프로젝트에:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>유효성 검사 및 비즈니스 논리 위반 처리

위의 유효성 검사 및 비즈니스 규칙 코드 만들기 또는 업데이트는 저녁에 언제 든 지 추가한, 했으므로 유효성 검사 논리 규칙을 평가 하 고 적용 합니다.

개발자 사전 유효 Dinner 개체 인지를 확인 하려면 아래와 같은 코드는 모든 예외를 생성 하지 않고 그 안에 모든 위반의 목록을 검색 합니다. 작성할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

잘못 된 상태에는 저녁 저장 하려고 하면, save () 메서드는 DinnerRepository에서 호출할 때 예외가 발생 합니다. 이 메서드는 저녁 변경 내용을 저장 하 고 Dinner에 존재 하는 규칙 위반 하는 경우 예외가 발생 하도록 Dinner.OnValidate()에 코드를 추가 했습니다 자동으로 LINQ to SQL 우리의 Dinner.OnValidate() 부분 메서드 호출 하기 때문에 발생 합니다. 이 예외를 catch 할 수 있으며 사후 문제를 해결 하려면 위반 목록에 검색 했습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

이 유효성 검사 및 비즈니스 규칙은 우리의 모델 계층 내에서 및 UI 계층 내에서 아닌를 구현 되므로 적용 되며 응용 프로그램 내에서 모든 시나리오에서 사용 합니다. 에서는 나중에 또는 비즈니스 규칙 추가 작동 하는 Dinner 개체 해당을 인식 하는 모든 코드를 있는 합니다.

를 한 곳에서 비즈니스 규칙을 변경할 수는 데 이러한 변경 내용은 응용 프로그램 및 UI 논리 전체 ripple 필요 없이 잘 작성 된 응용 프로그램과 것을 권장 하는 MVC 프레임 워크는 데 도움이 되는 이점이 기호입니다.

### <a name="next-step"></a>다음 단계

사용 하 여 쿼리하고 데이터베이스를 업데이트 하는 모델을 접수 이제 했습니다.

이제 추가해보겠습니다 컨트롤러와 뷰 일부 프로젝트에 테이블 주위의 HTML UI 경험을 만드는 데 사용할 수 있습니다.

> [!div class="step-by-step"]
> [이전](create-a-database.md)
> [다음](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
