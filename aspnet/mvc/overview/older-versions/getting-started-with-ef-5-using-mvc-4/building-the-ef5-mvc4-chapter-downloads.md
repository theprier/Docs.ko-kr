---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: 4 개의 자습서 5 EF MVC에 대 한 다운로드 장 구축 | Microsoft Docs
author: Rick-Anderson
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: fa018ea12929efa742a323d96938d372b634fdd7
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577070"
---
<a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>4 개의 자습서 5 EF MVC에 대 한 다운로드 장 빌드
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.


## <a name="building-the-chapter-downloads"></a>챕터 다운로드 빌드

1. 다운로드 하 고 프로젝트 샘플 zip 파일의 압축을 풉니다. 압축 푼된 다운로드 패키지에서 각 장의 완료에 대 한 추가 zip 파일을 찾을 수 있습니다.
2. 원하는 zip 파일을 마우스 오른쪽 단추로 클릭, 클릭 **속성**를 클릭 합니다 **차단 해제** 단추입니다.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. 파일을 압축을 풉니다.
4. 두 번 클릭 합니다 *CUx.sln* 파일을 Visual Studio를 시작 합니다.
5. **도구** 메뉴에서 클릭 **라이브러리 패키지 관리자**, 한 다음 **패키지 관리자 콘솔**합니다.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. 관리자 콘솔 (PMC (패키지)를 클릭 **복원**합니다.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Visual Studio를 끝냅니다.
8. 위의 단계에서 닫은 솔루션 파일을 열고 Visual Studio를 다시 시작 합니다.
9. 관리자 콘솔 (PMC (패키지)을 입력 합니다 `Update-Database` 명령:  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > 다음 오류가 발생 하면:  
    >   
    >  *' Update-database ' 용어는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식 되지 않습니다. 이름의 철자를 확인 하거나 경로 포함 하는 경우 경로가 올바른지 확인 하 고 다시 시도 합니다.*  
    > 종료 하 고 Visual Studio를 다시 시작 합니다.

    각 마이그레이션은 실행 한 다음 시드 메서드 실행 합니다. 이제 앱을 실행할 수 있습니다.

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [이전](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
