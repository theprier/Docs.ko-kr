---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: "검색 및 사용 하 여 데이터를 표시 합니다. 모델 바인딩 및 web forms | Microsoft Docs"
author: tfitzmac
description: "이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 데이터 상호 작용 하 게 더 많은 직선-중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: e750250285fcb0088da284588d721ac21e73820c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>검색 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 표시 합니다.
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 간단한 것 보다 데이터 상호 작용 하 게 합니다. 이 시리즈 소개 자료로 시작 하 고 이후의 자습서의 보다 발전된 된 개념 이동 합니다.
> 
> 모델 바인딩 패턴은 모든 데이터 액세스 기술을 사용 합니다. 이 자습서에서는 Entity Framework를 사용 하 여 하 이지만 가장 익숙한 데이터 액세스 기술에 사용할 수 있습니다. GridView, ListView, DetailsView, 또는 FormView 제어와 같은 데이터 바인딩된 서버 컨트롤에서 선택, 업데이트, 삭제 및 데이터 만들기에 대 한 사용 하는 방법의 이름을 지정 합니다. 이 자습서에서는 SelectMethod에 대 한 값을 지정 합니다.
> 
> 이 메서드 내에서 데이터를 검색 하기 위한 논리를 제공 합니다. 다음 자습서에서는 InsertMethod, UpdateMethod 및 DeleteMethod 한 값을 설정 합니다.
> 
> 있습니다 수 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트 다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013과 함께 작동합니다. 이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 차이가 있는 Visual Studio 2012 템플릿을 사용 합니다.
> 
> 자습서에서 Visual Studio에서 응용 프로그램을 실행 합니다. 또한 가능 응용 프로그램 사용 가능한 인터넷을 통해 호스팅 공급자에 게 배포 하 여 합니다. Microsoft에서 제공 하는 최대 10 개의 웹 사이트의 무료 웹 호스팅는  
>  [무료 Azure 평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다. Azure 앱 서비스 웹 앱에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 정보를 참조 하십시오.는 [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md) 계열입니다. 또한 해당 자습서는 Azure SQL 데이터베이스로 SQL Server 데이터베이스를 배포 하려면 Entity Framework Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Microsoft Visual Studio 2013 또는 Microsoft Visual Studio Express 2013 for Web
>   
> 
> 이 자습서에서는 Visual Studio 2012 에서도 작동 하지만 사용자 인터페이스와 프로젝트 템플릿에 차이가 됩니다.


## <a name="what-youll-build"></a>만들 것인지

이 자습서에서는 다음을 수행합니다.

1. 과목에 등록 하는 학습자와 함께 대학을 반영 하는 데이터 개체를 작성 합니다.
2. 빌드 개체에서 데이터베이스 테이블
3. 데이터베이스 테스트 데이터를 채우려면
4. Web form에 데이터 표시

## <a name="set-up-project"></a>프로젝트 설정

Visual Studio 2013에서 만들 새 **ASP.NET 웹 응용 프로그램** 호출 **ContosoUniversityModelBinding**합니다.

![프로젝트 만들기](retrieving-data/_static/image2.png)

Web Forms 서식 파일을 선택 하 고에서 기본 옵션입니다. 프로젝트를 설정 하는 확인을 클릭 합니다.

![web forms를 선택 합니다.](retrieving-data/_static/image3.png)

첫째, 몇 가지 사이트의 모양을 사용자 지정 하려면 약간 변경 하 게 됩니다. 열기는 **Site.Master** 파일을 찾아 내 ASP.NET 응용 프로그램 대신 Contoso 대학 포함 하도록 제목을 변경 합니다.

[!code-aspx[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

그런 다음에서 머리글 텍스트를 변경 **응용 프로그램 이름** 를 **Contoso 대학**합니다.

[!code-aspx[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

또한 Site.Master에서이 사이트와 관련이 있는 페이지에 반영 하기 위해 머리글에 표시 되는 탐색 링크를 변경 합니다. 필요 하지 것입니다는 **에 대 한** 페이지 또는 **연락처** 페이지 되었으므로 해당 링크를 제거할 수 있습니다. 대신, 해야 라는 페이지에 대 한 링크 **학생**합니다. 이 페이지 아직 만들지 않았습니다.

[!code-aspx[Main](retrieving-data/samples/sample3.aspx)]

저장 하 고 Site.Master를 닫습니다.

이제 학생 데이터를 표시 하기 위해 web form을 만들어야 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** 는 **새 항목**합니다. 선택 된 **마스터 페이지가 있는 웹 폼** 서식 파일을 하 고 이름을 **Students.aspx**합니다.

![페이지 만들기](retrieving-data/_static/image5.png)

선택 **Site.Master** 새 web form에 대 한 마스터 페이지로 합니다.

## <a name="create-the-data-models-and-database"></a>데이터 모델 및 데이터베이스 만들기

개체 및 해당 데이터베이스 테이블을 만드는 Code First 마이그레이션을 사용 합니다. 이러한 테이블에 학생과 해당 과정에 대 한 정보를 저장 됩니다.

모델 폴더에서 이라는 새 클래스 추가 **UniversityModels.cs**합니다.

![모델 클래스 만들기](retrieving-data/_static/image7.png)

이 파일에 SchoolContext, 학생, 회사 포털 등록, 및 과정 클래스를 다음과 같이 정의 합니다.

[!code-csharp[Main](retrieving-data/samples/sample4.cs)]

SchoolContext 클래스는 데이터베이스 연결 및 데이터의 변경 작업을 관리 하는 DbContext에서 파생 됩니다.

Student 클래스에서 특성에 적용 된을 확인는 **FirstName**, **LastName**, 및 **연도** 속성입니다. 이러한 특성은이 자습서의 데이터 유효성 검사에 사용 됩니다. 이 데모 프로젝트에 대 한 코드를 간소화 하기 위해 이러한 속성에만 데이터 유효성 검사 특성으로 표시 되었습니다. 실제 프로젝트에서 등록 및 과정 클래스의 속성 등의 유효성이 검사 된 데이터를 필요로 하는 모든 속성에 유효성 검사 특성을 적용 됩니다.

UniversityModels.cs를 저장 합니다.

이러한 클래스에 따라 데이터베이스를 설정 하려면 Code First 마이그레이션을 위한 도구를 사용 합니다.

**패키지 관리자 콘솔**, 명령을 실행 합니다.  
`enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

마이그레이션을 사용할 수 없다는 메시지가 나타납니다 명령이 성공적으로 완료 되는 경우

![마이그레이션을 사용 하도록 설정](retrieving-data/_static/image8.png)

새 파일의 이름이 사라졌는지 **Configuration.cs** 만들어졌습니다. Visual Studio에서이 파일을 만든 후 열 자동으로 됩니다. 구성 클래스를 포함 한 **시드** 메서드 테스트 데이터로 데이터베이스 테이블을 미리 채울 수 있습니다.

Seed 메서드를 다음 코드를 추가 합니다. 추가 해야 합니다는 **를 사용 하 여** 문에 **ContosoUniversityModelBinding.Models** 네임 스페이스입니다.

[!code-csharp[Main](retrieving-data/samples/sample5.cs)]

Configuration.cs를 저장 합니다.

패키지 관리자 콘솔에서 다음 명령을 실행 `add-migration initial`합니다.

그런 다음 명령을 실행 `update-database`합니다.

이 명령을 실행할 때 예외를 수신 경우 Seed 메서드 값에서 StudentID 및 CourseID 값에는 다양 한 수입니다. 데이터베이스에 해당 테이블을 열고 StudentID 및 CourseID에 대 한 기존 값을 찾습니다. 등록 테이블 시드를 위해 코드에서 해당 값을 추가 합니다.

데이터베이스 파일을 추가 되었지만 프로젝트에 숨겨져 있습니다. 클릭 **모든 파일 표시** 파일을 표시 합니다.

![모든 파일 표시](retrieving-data/_static/image10.png)

.Mdf 파일 이제 응용 프로그램에 나타납니다.\_데이터 폴더.

![데이터베이스 파일](retrieving-data/_static/image12.png)

.Mdf 파일을 두 번 클릭 하 고 서버 탐색기를 엽니다. 이제 테이블 존재 하 고 데이터로 채워집니다.

![데이터베이스 테이블](retrieving-data/_static/image14.png)

## <a name="display-data-from-students-and-related-tables"></a>학생 및 관련된 테이블의 데이터 표시

데이터베이스의 데이터로 준비가 이제 해당 데이터를 검색 하 고 웹 페이지에 표시 합니다. 사용 하 여 한 **GridView** 컨트롤을 데이터 열과 행에 표시 합니다.

Students.aspx를 열고 찾습니다는 **MainContent** 자리 표시자입니다. 자리 표시자를 내 추가 **GridView** 다음 코드를 포함 하는 컨트롤입니다.

[!code-aspx[Main](retrieving-data/samples/sample6.aspx)]

이 태그 코드를 감지 하는 데 중요 한 개념의 두 가지가 있습니다. 먼저, 값에 설정 되어 있는지 확인할 수는 **SelectMethod** GridView 요소의 속성입니다. 이 값에 GridView에 대 한 데이터를 검색 하기 위해 사용 되는 메서드의 이름을 지정 합니다. 이 메서드는 다음 단계에서 만들어집니다. 둘째, 여기서는 **ItemType** 앞에서 만든 Student 클래스 속성입니다. 이 값을 설정 하 여 태그 코드에 해당 클래스의 속성을 참조할 수 있습니다. 예를 들어 Student 클래스 등록 라는 컬렉션을 포함 합니다. 사용할 수 있습니다 **Item.Enrollments** 를 해당 컬렉션을 검색 하 고 다음 LINQ 구문을 사용 하 여 각 학생에 대해 등록 된 크레딧의 합계를 검색 합니다.

코드 숨김 파일에서에 대해 지정 된 메서드를 추가 해야는 **SelectMethod** 값입니다. 열기 **Students.aspx.cs**, 추가 **를 사용 하 여** 에 대 한 문을 **ContosoUniversityModelBinding.Models** 및 **System.Data.Entity**네임 스페이스입니다.

[!code-csharp[Main](retrieving-data/samples/sample7.cs)]

다음 메서드를 추가 합니다. 이 메서드의 이름을 SelectMethod에 대해 제공한 이름과 일치 하는지 확인 합니다.

[!code-csharp[Main](retrieving-data/samples/sample8.cs)]

**Include** 절이 쿼리의 성능이 향상 되지만 쿼리 작업을 위해 반드시 합니다. Include 절 없이 보내는 데이터베이스에 별도 쿼리가 각 시간 관련 데이터를 검색 하는 작업이 포함 된 지연 로드를 사용 하 여 데이터를 검색할 수는 있습니다. 또한 Include 절을 제공 하 여 데이터 관련된 데이터의 모든 데이터베이스의 단일 쿼리를 통해 검색 됩니다 즉 즉시 로드를 사용 하 여 검색 됩니다. 관련된 데이터의 대부분은 아닐 경우에 더 많은 데이터가 검색 되기 때문에 사용 되는, 즉시 로드 덜 효율적인 수 있습니다. 그러나이 경우 즉시 로드 최상의 성능을 제공 각 레코드에 대해 관련된 데이터 표시 되기 때문입니다.

로드할 때 성능 고려 사항에 대 한 자세한 내용은 관련 데이터에 대 한 섹션을 참조 하세요. **Lazy, Eager, 및 관련 데이터의 명시적 로드** 에 [는 ASP에서 Entity Framework와 관련 된 데이터 읽기 .NET MVC 응용 프로그램](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 항목입니다.

기본적으로 데이터 키로 표시 된 속성의 값에 따라 정렬 됩니다. 정렬에 대 한 다른 값을 지정 하려면 OrderBy 절을 추가할 수 있습니다. 이 예제에서는 기본 StudentID 속성이 정렬에 사용 됩니다. 에 [정렬, 페이징, 및 데이터 필터링](sorting-paging-and-filtering-data.md) 항목 정렬에 대 한 열을 선택 하려면 사용자를 사용할 수 있습니다.

웹 응용 프로그램을 실행 하 고 학생 페이지로 이동 합니다. 학생 페이지에는 다음 학생 정보가 표시 됩니다.

![데이터 표시](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>모델 바인딩 메서드를 자동으로 생성

이 자습서 시리즈를 작업할 때 프로젝트에 다음 자습서의 코드를 단순히 복사할 수 있습니다. 그러나 한 가지이 접근 방법의 단점은 자동으로 모델 바인딩 방법에 대 한 코드를 생성 하기 위해 Visual Studio에서 제공 하는 기능의 사실을 인식 하지 않을 수 있습니다. 사용자의 프로젝트를 사용할 때 자동 코드 생성 하면 시간 및 도움말 작업을 구현 하는 방법의 의미를 얻을 수 있습니다. 이 섹션에서는 자동 코드 생성 기능을 설명 합니다. 이 섹션에는 정보 제공만 고 프로젝트에 구현 하는 데 필요한 모든 코드가 포함 되지 않습니다.

에 대 한 값을 설정할 때의 **SelectMethod**, **UpdateMethod**, **InsertMethod**, 또는 **DeleteMethod** 태그 코드에서 속성 선택할 수는 **새 메서드 만들기** 옵션입니다.

![새 메서드 만들기](retrieving-data/_static/image18.png)

Visual Studio 적절 한 서명 사용 하 여 코드 숨김의 메서드를 만들고 뿐만 아니라도 작업을 수행 해야 하는지 구현 코드를 생성 합니다. 처음 설정 하는 경우는 **ItemType** 생성된 된 코드 자동 코드 생성 기능을 사용 하기 전에 속성을이 작업에 대 한 형식을 사용 합니다. 예를 들어, UpdateMethod 속성을 설정할 때 다음 코드가 자동으로 만들어집니다.

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

다시 위의 코드에서 프로젝트에 추가할 필요가 없습니다. 다음 자습서에서는 업데이트, 삭제 및 새 데이터를 추가 하기 위한 메서드를 구현 합니다.

## <a name="conclusion"></a>결론

이 자습서에서는 데이터 모델 클래스를 만들고 해당 클래스에서 데이터베이스를 생성 했습니다. 테스트 데이터를 데이터베이스 테이블을 채울. 모델 바인딩 데이터베이스에서 데이터를 검색 한 다음는 GridView에 데이터를 표시 합니다.

다음에서 [자습서](updating-deleting-and-creating-data.md) 이 시리즈의 업데이트, 삭제, 및 데이터를 만드는 사용 합니다.

>[!div class="step-by-step"]
[다음](updating-deleting-and-creating-data.md)
