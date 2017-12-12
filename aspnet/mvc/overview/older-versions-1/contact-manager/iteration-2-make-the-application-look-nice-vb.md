---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: "반복 #2-는 응용 프로그램의 좋은 (VB) 모양을 확인 | Microsoft Docs"
author: microsoft
description: "이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 07c4eaaf9ae5a389605a98951e970d410ca23122
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="iteration-2--make-the-application-look-nice-vb"></a>반복 #2-좋은 (VB)을 찾을 응용 프로그램으로 설정
====================
여 [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> 이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램 (VB) 빌드
  

이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다. 관리자에 게 문의 응용 프로그램을 사용 하면 연락처 정보를 저장-이름, 전화 번호 및 전자 메일 주소 – 목록에 대 한 사용자의 수 있습니다.

여러 반복을 통해에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.

- 반복 #1 – 응용 프로그램을 만듭니다. 첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-모양이 아닌 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- #3-추가 폼 유효성 검사를 반복 합니다. 세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소, 전화 번호를 확인 합니다.

- 반복 #4 – 느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다. 예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 6-테스트 기반 개발을 사용 합니다. 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복 메일 그룹을 추가합니다.

- #7 – 추가 Ajax 기능을 반복 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.

## <a name="this-iteration"></a>이 반복

이 반복의 목표 않아 응용 프로그램의 모양을 개선 하는 것입니다. 현재, 연락처 관리자는 기본 ASP.NET MVC 뷰 마스터 페이지 및 연계 스타일 시트 (그림 1 참조)를 사용 합니다. 이러한 안 불량, 보이지만 원하지 동일 하 게 다른 모든 ASP.NET MVC 웹 사이트를 않아 하지 않습니다. 사용자 지정 파일에 이러한 파일을 대체 하겠습니다.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**그림 01**: ASP.NET MVC 응용 프로그램의 기본 모양을 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image2.png))


이 반복 응용 프로그램의 시각적 디자인을 개선 하는 데 두 가지 방법에 설명 합니다. 첫째, 방법을 보여 무료 ASP.NET MVC 디자인 서식 파일을 다운로드 하려면 ASP.NET MVC 디자인 갤러리를 활용할 수 있습니다. ASP.NET MVC 디자인 갤러리를 사용 하는 작업을 수행 하지 않고 전문 웹 응용 프로그램을 만들 수 있습니다.

않아 응용 프로그램에 대 한 ASP.NET MVC 디자인 갤러리에서 서식 파일을 사용 하지 않도록 하기로 결정 합니다. 대신, 전문 디자인 회사에서 만든 사용자 지정 디자인을 했습니다. 이 자습서의 두 번째 부분에서 최종 ASP.NET MVC 디자인을 만드는 전문가 디자인 회사와 저는 각 I 설명 합니다.

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 디자인 갤러리

ASP.NET MVC 디자인 갤러리에는 Microsoft에서 제공 무료 리소스입니다. ASP.NET MVC 갤러리는 다음 주소에:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 디자인 갤러리 ASP.NET MVC 프로젝트에 사용 하기 위해 생성 된 무료 웹 사이트 디자인의 컬렉션을 호스트 합니다. 설계는 커뮤니티의 회원이 업로드 됩니다. 갤러리 방문자가 즐겨 찾는 설계에 대 한 투표 수 있습니다 (그림 2 참조).


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**그림 02**: The ASP.NET MVC 디자인 갤러리 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image4.png))


이 자습서를 쓰고 갤러리에서 가장 인기 있는 디자인 David Hauser 여 년 10 월 이라는 노드 구성입니다. 다음 단계를 완료 하 여 ASP.NET MVC 프로젝트에 대 한이 디자인을 사용할 수 있습니다.

1. 클릭는 **다운로드** 단추를 사용자 컴퓨터로 October.zip 파일을 다운로드 합니다.
2. 다운로드 한 October.zip 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭는 **차단 해제** 단추 (그림 3 참조).
3. 10 월 이라는 폴더에 파일을 압축을 풉니다.
4. 10 월 폴더에 포함 된 DesignTemplate 폴더에서 모든 파일을 선택 합니다. 해당 파일을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **복사**합니다.
5. Visual Studio 솔루션 탐색기 창에서 ContactManager 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **붙여넣기** (그림 4 참조).
6. Visual Studio 메뉴 옵션을 선택 **편집, 찾기 및 바꾸기, 빠른 바꾸기** 바꾸고 *[MyProjectName]* 와 *ContactManager* (그림 5 참조).


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**그림 03**:는 웹에서 다운로드 한 파일을 차단 해제 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image6.png))


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**그림 04**: 솔루션 탐색기에서 파일을 덮어쓰지 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image8.png))


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**그림 05**: ContactManager [이름] 경로로 바꿉니다 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image10.png))


다음이 단계를 완료 한 후 웹 응용 프로그램의 새로운 디자인을 사용 합니다. 그림 6에 있는 페이지와 년 10 월 디자인 않아 응용 프로그램의 모양을 보여 줍니다.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**그림 06**: ContactManager 년 10 월 템플릿으로 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image12.png))


## <a name="creating-a-custom-aspnet-mvc-design"></a>사용자 지정 ASP.NET MVC 디자인 만들기

ASP.NET MVC 디자인 갤러리 좋은 선택한 다른 디자인 스타일에 있습니다. 갤러리는 ASP.NET MVC 응용 프로그램의 모양을 사용자 지정할 수 있는 간편한 방법을 제공 합니다. 및 물론, 갤러리가 완전히 들지 큰 이점이 있습니다.

그러나 웹 사이트에 대 한 완전히 고유한 디자인을 만드는 할 수 있습니다. 이 경우에 웹 사이트 디자인 회사에서 실행 되도록 것이 좋습니다. 이 접근 방식을 않아 응용 프로그램에 대 한 디자인에 대 한 하기로 결정 합니다.

반복 # 1에서 연락처 관리자를 압축 하 고 설계 회사에 프로젝트를 전송 합니다. 해당 않았음에도 t 문제를 나타내지 (참에!), Visual Studio를 소유 하지 않았습니다. Microsoft Visual Web Developer를 무료로 다운로드할 수 있었던는 [https://www.asp.net](https://www.asp.net) 웹 사이트 및 Visual Web Developer에서 않아 응용 프로그램을 엽니다. 며칠, 그림 7에 디자인 얻은 결과 있습니다.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**그림 07**: ASP.NET MVC 않아 디자인 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image14.png))


두 가지 주요 파일 하는 구성 된 새로운 디자인: 새 연계 스타일 시트 파일 및 새 뷰 마스터 페이지 파일입니다. 뷰 마스터 페이지 레이아웃 및 ASP.NET MVC 응용 프로그램의 뷰에 대 한 공유 콘텐츠를 포함합니다. 예를 들어 뷰 마스터 페이지 그림 7에서는 머리글, 탐색 탭 및 표시 되는 바닥글을 포함 합니다. 설계 회사에서 새 Site.Master 파일 Views\Shared 폴더에서에서 기존 Site.Master 뷰 마스터 페이지를 덮어쓴 I

설계 회사 연계 새 스타일 시트 및 이미지의 집합에도 만들어집니다. 이러한 새 파일의 콘텐츠 폴더에 배치 하 고 기존 Site.css 파일을 덮어썼습니다. 콘텐츠 폴더에 모든 정적 콘텐츠를 넣어야 합니다.

Contact Manager에 대 한 새로운 디자인에 이미지를 편집 하 고 연락처 삭제를 확인 합니다. 연락처의 HTML 테이블에 각 연락처 옆으로 편집 및 삭제 이미지로가 나타납니다.

HTML 렌더링 된 다음 링크를 원래, 합니다. 다음과 같은 도우미 ActionLink():

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.ActionLink() 메서드 (HTML 메서드 보안상의 이유로 대 한 링크 텍스트를 인코딩합니다) 이미지를 지원 하지 않습니다. 따라서 다음과 같이 Url.Action() 호출 하 여 Html.ActionLink()에 대 한 호출을 교체 I.

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Html.ActionLink() 메서드는 전체 HTML 하이퍼링크를 렌더링합니다. Url.Action() 메서드 반면에 렌더링 하는 URL만 하지 않고는 &lt;는&gt; 태그입니다.

또한 새로운 디자인에 선택 및 선택 되지 않은 탭이 포함 되어 있는지 확인할 수입니다. 그림 8의 예를 들어는 **새 연락처 만들기** 탭을 선택 및 **내 연락처** 탭이 선택 되지 않습니다.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**그림 08**: 선택한 탭을 선택 하지 않은 ([전체 크기 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image16.png))


선택 및 선택 되지 않은 탭 렌더링를 지원 하기 위해 필자는 MenuItemHelper 라는 사용자 지정 HTML 도우미를 만들었습니다. 이 도우미 메서드를 렌더링 하거나는 &lt;li&gt; 태그 또는 &lt;li 클래스 "선택" =&gt; 현재 컨트롤러 및 작업 도우미에 전달 된 컨트롤러 및 작업 이름에 해당 하는 여부에 따라 태그입니다. MenuItemHelper에 대 한 코드 목록 1에 포함 됩니다.

**1 – Helpers\MenuItemHelper.vb 나열**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper를 사용 하 여 TagBuilder 클래스 내부적으로 작성 된 &lt;li&gt; HTML 태그입니다. TagBuilder 클래스는 새 HTML 태그를 작성 해야 할 때마다 사용할 수 있는 매우 유용한 유틸리티 클래스입니다. 특성을 추가, CSS 클래스를 추가 하 고, Id, 생성 하 고 s 태그를 수정 하기 위한 메서드 포함 내부 HTML입니다.

## <a name="summary"></a>요약

이 반복에 ASP.NET MVC 응용 프로그램의 시각적 디자인을 개선 했습니다. 첫째, ASP.NET MVC 디자인 갤러리에 도입 된 있습니다. ASP.NET MVC 응용 프로그램에서 사용할 수 있는 ASP.NET MVC 디자인 갤러리에서 무료 디자인 서식 파일을 다운로드 하는 방법을 배웠습니다.

다음으로, 기본 연계 스타일 시트 파일 및 마스터 뷰 페이지 파일을 수정 하 여 사용자 지정 디자인을 만들 수는 방법을 설명 합니다. 새 디자인을 지원 하기 위해 몇 가지 사소한 변경 않아 응용 프로그램을 만들어야 했습니다. 예를 들어 라는 MenuItemHelper 또는 선택 하지 않은 탭이 표시 되는 새 HTML 도우미를 추가 했습니다.

다음 반복에서 유효성 검사의 매우 중요 한 주제를 해결할 했습니다. 사용자 먼저 사용자 s 등 필요한 값을 제공 하지 않고 새 연락처를 만들 수 없습니다 및 성을 유효성 검사 코드에 응용 프로그램을 추가 했습니다.

>[!div class="step-by-step"]
[이전](iteration-1-create-the-application-vb.md)
[다음](iteration-3-add-form-validation-vb.md)
