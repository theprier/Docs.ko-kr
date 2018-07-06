---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: 모델, 뷰 및 컨트롤러 이해 (C#) | Microsoft Docs
author: StephenWalther
description: 모델, 뷰 및 컨트롤러에 대 한 자세한 내용은 이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램의 여러 부분을 소개합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: f5cf39e4652a3e487dcd79b2cf887efb992c2107
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376911"
---
<a name="understanding-models-views-and-controllers-c"></a>모델, 뷰 및 컨트롤러 이해 (C#)
====================
[Stephen walther가](https://github.com/StephenWalther)

> 모델, 뷰 및 컨트롤러에 대 한 자세한 내용은 이 자습서에서는 Stephen walther가 ASP.NET MVC 응용 프로그램의 여러 부분을 소개합니다.


이 자습서 모델, 뷰 및 컨트롤러 수와 ASP.NET MVC의 대략적인 개요를 제공합니다. 즉, M을 설명 합니다 ', V', c ' ASP.NET MVC에서.

이 자습서를 읽은 후 ASP.NET MVC 응용 프로그램의 다른 부분이 함께 작동 하는 방법을 이해 해야 합니다. 또한 ASP.NET Web Forms 응용 프로그램 또는 Active Server Pages 응용 프로그램에서 ASP.NET MVC 응용 프로그램의 아키텍처 차이점을 이해 해야 합니다.

## <a name="the-sample-aspnet-mvc-application"></a>샘플 ASP.NET MVC 응용 프로그램

ASP.NET MVC 웹 응용 프로그램을 만들기 위한 기본 Visual Studio 템플릿은 ASP.NET MVC 응용 프로그램의 다른 부분을 이해 하는 매우 간단한 샘플 응용 프로그램을 포함 합니다. 이 자습서의이 간단한 응용 프로그램의 활용 했습니다.

Visual Studio 2008을 실행 하 여 MVC 템플릿을 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들면 및 파일 메뉴 옵션을 선택 하면, 새 프로젝트 (그림 1 참조). 새 프로젝트 대화 상자에서 프로젝트 형식 (Visual Basic 또는 C#)에서 원하는 프로그래밍 언어를 선택 하 고 선택 **ASP.NET MVC 웹 응용 프로그램** 템플릿에서 합니다. 확인 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

**그림 01**: 새 프로젝트 대화 상자 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-cs/_static/image2.png))


새 ASP.NET MVC 응용 프로그램을 만들 때 합니다 **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다 (그림 2 참조). 이 대화 상자를 사용 하면 ASP.NET MVC 응용 프로그램을 테스트 하는 것에 대 한 솔루션에 별도 프로젝트를 만들 수 있습니다. 옵션을 선택 **아니요, 단위 테스트 프로젝트를 만들지 않습니다** 을 클릭 합니다 **확인** 단추입니다.


[![단위 테스트 대화 상자 만들기](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

**그림 02**: 단위 테스트 만들기 대화 상자 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-cs/_static/image4.png))


새 ASP.NET MVC 후 응용 프로그램이 만들어집니다. 솔루션 탐색기 창에서 여러 파일과 폴더 표시 됩니다. 특히, 모델, 뷰 및 컨트롤러 라는 세 개의 폴더가 표시 됩니다. 폴더 이름에서 추측할 수 있습니다,으로 이러한 폴더는 모델, 뷰 및 컨트롤러를 구현 하는 것에 대 한 파일을 포함 합니다.

컨트롤러 폴더를 확장 하면 AccountController.cs 이라는 파일과 HomeController.cs 파일 표시 됩니다. Views 폴더를 확장 하는 경우 명명 된 계정에 홈 및 공유 하는 세 개의 하위 폴더 표시 됩니다. 홈 폴더를 확장 하면 About.aspx 및 Index.aspx (그림 3 참조) 라는 추가 파일 두 개가 표시 됩니다. 이러한 파일은 기본 ASP.NET MVC 템플릿 사용 하 여 포함 된 샘플 응용 프로그램을 구성 합니다.


[![솔루션 탐색기 창](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

**그림 03**:의 솔루션 탐색기 창 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-cs/_static/image6.png))


메뉴 옵션을 선택 하 여 샘플 응용 프로그램을 실행할 수 있습니다 **디버그, 디버깅 시작**합니다. 또는 F5 키를 눌러 수 있습니다.

ASP.NET 응용 프로그램을 처음으로 실행 하는 경우 디버그 모드를 사용 하는 것이 좋습니다. 그림 4의 대화 상자가 나타납니다. 확인 단추를 클릭 하 고 응용 프로그램이 실행 됩니다.


[![디버깅 해제 대화 상자](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

**그림 04**: 디버깅 사용 안 함 대화 상자 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-cs/_static/image8.png))


ASP.NET MVC 응용 프로그램을 실행 하면 Visual Studio 웹 브라우저에서 응용 프로그램을 실행 합니다. 샘플 응용 프로그램은 두 개의 페이지로 구성 되어 있습니다: 인덱스 페이지와 정보 페이지입니다. 응용 프로그램이 처음 시작 하는 경우 인덱스 페이지가 나타납니다 (그림 5 참조). 정보 페이지 맨 위에 있는 메뉴 링크를 클릭 하 여 이동할 응용 프로그램의 오른쪽입니다.


[![인덱스 페이지](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

**그림 05**:은 인덱스 페이지 ([큰 이미지를 보려면 클릭](understanding-models-views-and-controllers-cs/_static/image11.png))


브라우저의 주소 표시줄에 Url을 확인 합니다. 예를 들어 정보 메뉴 링크를 클릭 하면 브라우저 주소 표시줄에서 URL 변경 **/Home/에 대 한**합니다.

브라우저 창을 닫고 Visual Studio로 돌아가서 경우 경로 홈/에 대 한 파일을 찾을 수 없습니다. 파일이 존재 하지 않습니다. 어떻게 이것이 가능 한가요?

## <a name="a-url-does-not-equal-a-page"></a>URL 페이지와 같지 않습니다.

기존의 ASP.NET Web Forms 응용 프로그램 또는 Active Server Pages 응용 프로그램을 빌드할 때 URL 및 페이지 간의 한 일 대응이 됩니다. 서버의 SomePage.aspx 라는 페이지를 요청 하는 경우 다음 했습니다 더 있을 페이지 SomePage.aspx 라는 디스크. 좋지 않은 SomePage.aspx 파일이 없으면 얻게 **404-페이지를 찾을 수 없음** 오류입니다.

ASP.NET MVC 응용 프로그램을 빌드하는 경우 반면 없습니다 대응이 됩니다 브라우저의 주소 표시줄에 입력 하는 URL 및 응용 프로그램에서 발견 하는 파일입니다. ASP.NET MVC 응용 프로그램에 URL을 디스크에 페이지 대신 컨트롤러 작업에 해당합니다.

기존 ASP 또는 ASP.NET 응용 프로그램, 브라우저 요청 페이지에 매핑됩니다. 반면에 ASP.NET MVC 응용 프로그램에서 브라우저 요청 컨트롤러 작업에 매핑됩니다. ASP.NET Web Forms 응용 프로그램은 콘텐츠 중심입니다. ASP.NET MVC 응용 프로그램에 반대로 중심 응용 프로그램 논리 이며

## <a name="understanding-aspnet-routing"></a>ASP.NET 라우팅 이해

브라우저 요청을 호출 하는 ASP.NET 프레임 워크의 기능을 통해 컨트롤러 작업에 매핑하여 *ASP.NET 라우팅에서*합니다. ASP.NET 라우팅은 ASP.NET MVC 프레임 워크에서 사용 됩니다 *경로* 컨트롤러 작업에 들어오는 요청.

ASP.NET 라우팅 들어오는 요청을 처리 하는 경로 테이블을 사용 합니다. 이 경로 테이블에는 웹 응용 프로그램을 처음 시작할 때 생성 됩니다. 경로 테이블이 Global.asax 파일에 설치 합니다. 기본 MVC Global.asax 파일 목록 1에 포함 됩니다.

**목록 1-Global.asax**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

ASP.NET 응용 프로그램을 처음 시작 되 면 응용 프로그램\_start () 메서드가 호출 됩니다. 목록 1에서이 메서드는 RegisterRoutes() 메서드를 호출 하 고 RegisterRoutes() 메서드 기본 경로 테이블을 만듭니다.

하나의 경로 기본 경로 테이블로 구성 됩니다. 이 기본 경로 (URL 세그먼트는 슬래시 사이 있는 것)는 세 개의 선분으로 들어오는 모든 요청을 중단 합니다. 첫 번째 세그먼트는 컨트롤러 이름에 매핑된, 두 번째 세그먼트는 작업 이름으로 매핑되고 최종 세그먼트는 id 라는 이름의 작업에 전달 된 매개 변수에 매핑됩니다.

예를 들어 다음 URL을 가정해 봅니다.

/ 제품/세부 정보/3

이 URL은 다음과 같은 세 개의 매개 변수를 구문 분석 됩니다.

컨트롤러 = 제품

작업 세부 정보 =

id = 3

Global.asax 파일에 정의 된 기본 경로 세 매개 변수 모두에 대 한 기본 값을 포함 합니다. 기본 컨트롤러는 홈, 기본 작업은 인덱스 및 Id 기본값은 빈 문자열입니다. 염두에서 이러한 기본값을 사용 하 여 다음 URL을 구문 분석 방법을 하는 것이 좋습니다.

/ 직원

이 URL은 다음과 같은 세 개의 매개 변수를 구문 분석 됩니다.

컨트롤러 직원 =

작업 = 인덱스

Id =

마지막으로, 모든 URL을 제공 하지 않고 ASP.NET MVC 응용 프로그램을 열면 (예를 들어 `http://localhost`) URL은 다음과 같은 구문 분석:

컨트롤러 = 홈

작업 = 인덱스

Id =

HomeController 클래스에 대 한 index () 동작 요청이 라우팅됩니다.

## <a name="understanding-controllers"></a>컨트롤러의 이해

컨트롤러는 MVC 응용 프로그램을 사용 하 여 사용자 상호 작용 하는 방법을 제어 하는 일을 담당 합니다. 컨트롤러에는 ASP.NET MVC 응용 프로그램에 대 한 흐름 제어 논리를 포함합니다. 컨트롤러는 사용자 브라우저 요청을 수행 하는 경우 사용자에 게 다시 보낼 어떤 응답을 결정 합니다.

컨트롤러는 방금 클래스 (예를 들어, Visual Basic 또는 C# 클래스). 샘플 ASP.NET MVC 응용 프로그램 컨트롤러 폴더에 있는 HomeController.cs 라는 컨트롤러를 포함 합니다. HomeController.cs 파일의 내용은 나열 하는 2에서 재생성 됩니다.

**2-HomeController.cs 나열**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

HomeController index () 및 about () 라는 두 가지 방법에 있는지 확인 합니다. 이러한 두 메서드는 컨트롤러에 의해 노출 되는 두 가지 작업에 해당 합니다. URL /Home/인덱스 HomeController.Index() 메서드를 호출 하 고 URL /Home/About HomeController.About() 메서드를 호출 합니다.

모든 public 메서드를 컨트롤러의 컨트롤러 작업으로 노출 됩니다. 이 대해 주의 해야 합니다. 이 브라우저에 올바른 URL을 입력 하 여 인터넷에 액세스할 수 있는 모든 사용자가 컨트롤러에 포함 된 모든 public 메서드를 호출할 수 있음을 의미 합니다.

## <a name="understanding-views"></a>뷰 이해

HomeController 클래스, index () 및 about ()에 의해 노출 된 두 명의 컨트롤러 작업 뷰를 둘 다 반환 합니다. 뷰를 HTML 태그 및 브라우저에 전송 되는 콘텐츠를 포함 합니다. 보기는 페이지에 해당 하는 경우 ASP.NET MVC 응용 프로그램을 사용 합니다.

적절 한 위치에서 보기를 만들어야 합니다. HomeController.Index() 작업에는 다음 경로에 있는 뷰를 반환 합니다.

\Views\Home\Index.aspx

HomeController.About() 작업에는 다음 경로에 있는 뷰를 반환 합니다.

\Views\Home\About.aspx

일반적으로 컨트롤러 작업에 대 한 뷰를 반환 하려는 경우 다음 해야 컨트롤러와 동일한 이름 가진 Views 폴더의 하위 폴더를 만듭니다. 하위 폴더 내에서 컨트롤러 작업으로 동일한 이름을 가진.aspx 파일을 만들어야 합니다.

보기 3의 파일 about.aspx로 뷰를 포함합니다.

**3-About.aspx 나열**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

보기 3의 첫 번째 줄을 무시 하면 보기의 나머지 부분은 대부분 표준 HTML 이루어져 있습니다. 여기에 원하는 모든 HTML 입력 하 여 보기의 콘텐츠를 수정할 수 있습니다.

뷰는 Active Server Pages에서 ASP.NET Web Forms 페이지와 매우 비슷합니다. 뷰를 HTML 콘텐츠와 스크립트에 포함할 수 있습니다. 원하는.NET에서 프로그래밍 언어 (예를 들어 C# 또는 Visual Basic.NET) 스크립트를 작성할 수 있습니다. 스크립트를 사용 하 여 데이터베이스 데이터와 같은 동적 콘텐츠를 표시 합니다.

## <a name="understanding-models"></a>모델 이해

컨트롤러에서 설명한 및 뷰를 살펴보았습니다. 모델을 설명 해야 하는 마지막 항목입니다. MVC 모델 이란?

MVC 모델을 모든 뷰 또는 컨트롤러에 포함 되지 않은 응용 프로그램 논리를 포함 합니다. 모델에 모든 응용 프로그램 비즈니스 논리, 유효성 검사 논리 및 데이터베이스 액세스 논리를 포함 해야 합니다. 예를 들어,를 사용 하 여 데이터베이스에 액세스 Microsoft Entity Framework를 사용 하는 경우 다음은 Entity Framework 클래스 (.edmx 파일)에서 만든 Models 폴더입니다.

보기와 관련 된 사용자 인터페이스를 생성 하는 논리만 포함 해야 합니다. 컨트롤러의 오른쪽 보기를 반환 하거나 다른 작업 (흐름 제어)에 사용자를 리디렉션하는 데 필요한 논리는 최소 사항만 포함 해야 합니다. 다른 모든 모델에 포함 되어야 합니다.

일반적으로 fat 모델과 스키 니 컨트롤러를 높여야 합니다. 컨트롤러 메서드는 코드 몇 줄만 포함 해야 합니다. 컨트롤러 작업을 가져옵니다 너무 fat, 논리를 Models 폴더에 새 클래스 이동 고려해 야 있습니다.

## <a name="summary"></a>요약

이 자습서 웹 응용 프로그램을 ASP.NET MVC의 여러 부분의 높은 수준의 개요를 제공 합니다. ASP.NET 라우팅에서 매핑되는 방식을 들어오는 브라우저 요청 특정 컨트롤러 작업에 배웠습니다. 뷰를 브라우저에 반환 되는 방법을 컨트롤러를 오케스트레이션 하는 방법을 배웠습니다. 마지막으로 모델 응용 프로그램 비즈니스, 유효성 검사 및 데이터베이스 액세스 논리를 포함 하는 방법을 배웠습니다.
