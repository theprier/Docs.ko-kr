---
title: ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기
author: rick-anderson
description: ASP.NET Core MVC 및 Windows용 Visual Studio를 사용하여 Web API 빌드
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/17/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-web-api
ms.openlocfilehash: 1680d5e0be0f4844c904d923af30634c53bd1b81
ms.sourcegitcommit: 9a35906446af7ffd4ccfc18daec38874b5abbef7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "34306675"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-windows"></a>ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)

이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다. UI(사용자 인터페이스)는 만들어지지 않습니다.

이 자습서는 다음 세 가지 버전으로 제공됩니다.

* Windows: Windows용 Visual Studio를 사용한 Web API(이 자습서)
* macOS: [Mac용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api-mac)
* macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a>전제 조건

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="create-the-project"></a>프로젝트를 만듭니다.

Visual Studio에서 다음 단계를 수행합니다.

* **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.
* **ASP.NET Core 웹 응용 프로그램** 템플릿을 선택합니다. 프로젝트 이름을 *TodoApi*로 지정하고 **확인**을 클릭합니다.
* **새 ASP.NET Core 웹 응용 프로그램 - TodoApi** 대화 상자에서 ASP.NET Core 버전을 선택합니다. **API** 템플릿을 선택하고 **확인**을 클릭합니다. **Docker 지원 사용**을 선택하지 **마세요**.

### <a name="launch-the-app"></a>앱 시작

Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다. Visual Studio가 브라우저를 시작하고 `http://localhost:<port>/api/values`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다. Chrome, Microsoft Edge 및 Firefox에는 다음 출력이 표시됩니다.

```json
["value1","value2"]
```

Internet Explorer를 사용 중인 경우 *values.json* 파일을 저장하라는 메시지가 표시됩니다.

### <a name="add-a-model-class"></a>모델 클래스 추가

모델은 앱의 데이터를 나타내는 개체입니다. 이 경우 유일한 모델은 할 일 항목입니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다. **추가** > **새 폴더**를 선택합니다. 폴더 이름을 *Models*로 지정합니다.

> [!NOTE]
> 모델 클래스는 프로젝트의 어디에서나 사용될 수 있습니다. *Models* 폴더는 모델 클래스에 대한 규칙에 사용됩니다.

솔루션 탐색기에서 *Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다. 클래스 이름을 *TodoItem*으로 지정하고 **추가**를 클릭합니다.

`TodoItem` 클래스를 다음 코드로 업데이트합니다.

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.

### <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다. `Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.

솔루션 탐색기에서 *Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다. 클래스 이름을 *TodoContext*로 지정하고 **추가**를 클릭합니다.

클래스를 다음 코드로 바꿉니다.

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a>컨트롤러 추가

솔루션 탐색기에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭합니다. **추가** > **새 항목**을 선택합니다. **새 항목 추가** 대화 상자에서 **API 컨트롤러 클래스** 템플릿을 선택합니다. 클래스 이름을 *TodoController*로 지정하고 **추가**를 클릭합니다.

![검색 상자의 컨트롤러 및 Web API 컨트롤러가 선택된 새 항목 추가 대화 상자](first-web-api/_static/new_controller.png)

클래스를 다음 코드로 바꿉니다.

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a>앱 시작

Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다. Visual Studio가 브라우저를 시작하고 `http://localhost:<port>/api/values`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다. `http://localhost:<port>/api/todo`의 `Todo` 컨트롤러로 이동합니다.

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
