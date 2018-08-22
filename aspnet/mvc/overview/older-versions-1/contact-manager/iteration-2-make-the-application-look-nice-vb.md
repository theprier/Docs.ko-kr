---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: '반복 #2 – 응용 프로그램 모양 꾸미기 (VB)를 확인 | Microsoft Docs'
author: microsoft
description: 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 7f27cbab17effc3b44649e06409893e6be09b011
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828535"
---
<a name="iteration-2--make-the-application-look-nice-vb"></a>반복 #2 – 응용 프로그램 모양 꾸미기 (VB) 확인
====================
[Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (VB)
  

이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다. 연락처 관리자 응용 프로그램을 사용 하면 연락처 정보 – 이름, 전화 번호 및 전자 메일 주소 – 목록에 대 한 사용자를 저장할 수 있습니다.

여러 반복에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.

- 반복 #1 – 응용 프로그램을 만듭니다. 첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2 – 보기 좋게 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사 추가 합니다. 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.

- 반복 #4 – 응용 프로그램을 느슨하게 결합을 확인 합니다. 이 네 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다. 예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 #6-테스트 중심 개발을 사용 합니다. 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복에서는 메일 그룹을 추가합니다.

- 반복 #7 – Ajax 기능 추가입니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.

## <a name="this-iteration"></a>이 반복

이 반복의 목표는 연락처 관리자 응용 프로그램의 모양을 향상 시킬 것입니다. 현재, Contact Manager는 기본 ASP.NET MVC 뷰 마스터 페이지 및 연계 스타일 시트 (그림 1 참조)를 사용 합니다. 이러한 안 불량, 보이지만 t 원하는 모든 다른 ASP.NET MVC 웹 사이트와 마찬가지로 검색할 Contact Manager 하지 않습니다. 사용자 지정 파일을 사용 하 여 이러한 파일을 대체 하려고 합니다.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**그림 01**: ASP.NET MVC 응용 프로그램의 기본 모양을 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image2.png))


이 반복 응용 프로그램의 시각적 디자인을 향상 시키기 위한 두 가지 방법에 설명 합니다. 먼저 하겠습니다 무료 ASP.NET MVC 디자인 템플릿을 다운로드 하기 위해 ASP.NET MVC 디자인 갤러리를 활용 하는 방법. ASP.NET MVC 디자인 갤러리를 사용 하면 모든 작업을 수행 하지 않고 전문 웹 응용 프로그램을 만들 수 있습니다.

연락처 관리자 응용 프로그램에 대 한 ASP.NET MVC 디자인 갤러리에서 템플릿을 사용 하기로 했습니다. 대신, 전문 디자인 회사에서 만든 사용자 지정 디자인을 했습니다. 이 자습서의 2 부에서 최종 ASP.NET MVC 디자인을 만들려면 전문 디자인 회사를 사용 하 여 필자가 하는 방법을 설명 하겠습니다.

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 디자인 갤러리

ASP.NET MVC 디자인 갤러리는 Microsoft에서 제공 하는 무료 리소스입니다. ASP.NET MVC 갤러리 다음 주소에 위치한:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 디자인 갤러리는 ASP.NET MVC 프로젝트에서 사용 하기 위해 생성 된 무료 웹 사이트 디자인의 컬렉션을 호스팅합니다. 디자인은 커뮤니티의 회원이 업로드 됩니다. 갤러리에는 방문자가 즐겨 찾는 설계에 대해 투표할 수 (그림 2 참조).


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**그림 02**: The ASP.NET MVC 디자인 갤러리 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image4.png))


이 자습서를 작성 하는 대로 갤러리에서 가장 인기 있는 디자인은 David Hauser 여 년 10 월 이라는 디자인 합니다. 다음 단계를 완료 하 여 ASP.NET MVC 프로젝트에 대 한이 디자인을 사용할 수 있습니다.

1. 클릭 합니다 **다운로드** October.zip 파일을 컴퓨터에 다운로드 하려면 단추입니다.
2. 다운로드 한 October.zip 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭 합니다 **차단 해제** 단추 (그림 3 참조).
3. 10 월 라는 폴더에 파일을 압축을 풉니다.
4. 10 월 폴더에 포함 된 DesignTemplate 폴더에서 모든 파일을 선택 합니다. 파일을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **복사**합니다.
5. Visual Studio 솔루션 탐색기 창에서 ContactManager 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **붙여넣기** (그림 4 참조).
6. Visual Studio 메뉴 옵션을 선택 **편집, 찾기 및 바꾸기, 빠른 바꾸기** 바꾸고 *[MyProjectName]* 사용 하 여 *ContactManager* (그림 5 참조).


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**그림 03**: 웹에서 다운로드 한 파일을 차단 해제 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image6.png))


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**그림 04**: 솔루션 탐색기에서 파일을 덮어쓸 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image8.png))


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**그림 05**: [ProjectName] ContactManager 바꿉니다 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image10.png))


다음이 단계를 완료 한 후 웹 응용 프로그램의 새로운 디자인을 사용 합니다. 그림 6에서 페이지 년 10 월 디자인을 사용 하 여 연락처 관리자 응용 프로그램의 모양을 보여 줍니다.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**그림 06**: ContactManager 년 10 월 템플릿 사용 하 여 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image12.png))


## <a name="creating-a-custom-aspnet-mvc-design"></a>사용자 지정 ASP.NET MVC 디자인 만들기

ASP.NET MVC 디자인 갤러리에는 다양 한 디자인 스타일 좋은 선택입니다. 갤러리는 ASP.NET MVC 응용 프로그램의 모양을 사용자 지정할 수 있는 간편한 방법을 제공 합니다. 그리고 물론 갤러리에 큰 장점이 완전히 무료로 제공 합니다.

그러나 웹 사이트에 대 한 완전히 고유한 설계를 만들 수 해야 합니다. 이런 경우는 웹 사이트 디자인 회사를 사용 하려면 것이 좋습니다. 연락처 관리자 응용 프로그램 디자인에 대 한이 방법을 사용 하기로 했습니다.

반복 # 1의 연락처 관리자를 압축 하 고 프로젝트 디자인 회사에 전송 합니다. 이러한 동작 t 문제가 없는 (아깝다는 에서도!), Visual Studio를 소유 하지 않았습니다. Microsoft Visual Web Developer를 무료로 다운로드할 수 있었습니다 합니다 [ https://www.asp.net ](https://www.asp.net) 웹 사이트 및 Visual Web Developer에서 연락처 관리자 응용 프로그램을 엽니다. 몇 일, 이러한 그림 7의 설계를 생성 했습니다.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**그림 07**: ASP.NET MVC Contact Manager 디자인 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image14.png))


두 개의 주 파일의 새 디자인은: 새 연계 스타일 시트 파일 및 새 보기 마스터 페이지 파일입니다. 보기 마스터 페이지 레이아웃 및 ASP.NET MVC 응용 프로그램의 보기에 대 한 공유 콘텐츠를 포함합니다. 예를 들어, 보기 마스터 페이지 그림 7에 헤더, 탐색 탭 및 표시 되는 바닥글을 포함 합니다. Views\Shared 폴더에서 기존 Site.Master 뷰 마스터 페이지 디자인 회사에서 새 Site.Master 파일을 사용 하 여 덮어쓴 있나요

디자인 회사 연계 하는 새 스타일 시트 및 이미지 집합에도 만들어집니다. 콘텐츠 폴더에 이러한 새 파일을 배치 하 고 기존 Site.css 파일을 덮어썼습니다. 콘텐츠 폴더에 모든 정적 콘텐츠를 배치 해야 합니다.

새 디자인에서는 대화 상대 관리자에 대 한 이미지 편집 하 고 연락처를 삭제 하는 중에 알 수 있습니다. 연락처의 HTML 테이블에 있는 각 연락처 옆에 있는 편집 및 삭제 이미지로가 나타납니다.

HTML을 사용 하 여 렌더링 된 다음 링크를 원래 합니다. 이와 같은 ActionLink() 도우미:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.ActionLink() 메서드 (HTML 메서드는 보안상의 이유로 링크 텍스트를 인코드) 이미지를 지원 하지 않습니다. 따라서 같이 Url.Action() 호출 하 여 Html.ActionLink()에 대 한 호출을 대체 하나요:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Html.ActionLink() 메서드는 전체 HTML 하이퍼링크를 렌더링합니다. Url.Action() 메서드 없이 URL만을 다른 한편으로 렌더링 합니다 &lt;는&gt; 태그입니다.

표시, 또한 새 디자인 탭을 선택 또는 선택 하지 않은 포함 합니다. 예를 들어, 그림 8에에서는 **새 연락처 만들기** 탭을 선택 하며 **내 연락처** 탭을 선택 하지 않으면.


[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**그림 08**: 선택한 탭을 선택 취소 ([큰 이미지를 보려면 클릭](iteration-2-make-the-application-look-nice-vb/_static/image16.png))


탭을 선택 또는 선택 하지 않은 렌더링을 지원 하려면 사용자 지정 HTML 도우미는 MenuItemHelper 라는 만들었습니다. 이 도우미 메서드를 렌더링 중 하나를 &lt;li&gt; 태그 또는 &lt;li 클래스 "선택" =&gt; 현재 컨트롤러 및 작업 도우미에 전달 된 컨트롤러 및 작업 이름에 해당 하는 여부에 따라 태그입니다. MenuItemHelper에 대 한 코드는 목록 1에 포함 됩니다.

**1 – Helpers\MenuItemHelper.vb 나열**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper 클래스를 사용 하는 TagBuilder 내부적으로 작성 하는 &lt;li&gt; HTML 태그입니다. TagBuilder 클래스는 새 HTML 태그를 작성 해야 할 경우 사용할 수 있는 매우 유용한 유틸리티 클래스입니다. 여기에 특성 추가, CSS 클래스를 추가, Id, 생성 및 s 태그를 수정 하기 위한 메서드 내부 HTML입니다.

## <a name="summary"></a>요약

이 반복에서 ASP.NET MVC 응용 프로그램의 시각적 디자인을 개선 했습니다. 먼저, ASP.NET MVC 디자인 갤러리를 소개 했습니다. ASP.NET MVC 응용 프로그램에서 사용할 수 있는 ASP.NET MVC 디자인 갤러리에서 무료 디자인 템플릿을 다운로드 하는 방법을 알아보았습니다.

다음으로, 기본 연계 스타일 시트 파일 및 마스터 뷰 페이지 파일을 수정 하 여 사용자 지정 디자인을 만드는 방법을 설명 합니다. 새 디자인을 지원 하기 위해 연락처 관리자 응용 프로그램에 일부 사소한 변경을 수행 해야 했습니다. 예를 들어 MenuItemHelper 또는 선택 하지 않은 탭이 표시 되는 명명 된 새 HTML 도우미를 추가 했습니다.

다음 반복에서는 유효성 검사의 매우 중요 한 주제를 수행할 수 있습니다. 사용자 수 없습니다. 새 연락처를 먼저 사용자가 등 필요한 값을 제공 하지 않고 만들고 있는 성 응용 프로그램 유효성 검사 코드를 추가 합니다.

> [!div class="step-by-step"]
> [이전](iteration-1-create-the-application-vb.md)
> [다음](iteration-3-add-form-validation-vb.md)
