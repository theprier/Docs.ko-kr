---
title: "개별 사용자 계정을 사용 하 여 만든 프로젝트를 기반으로 문서"
author: rick-anderson
description: "이 문서는 개별 사용자 계정을 사용 하 여 만든 프로젝트를 기반으로 문서를 나열 합니다."
keywords: "ASP.NET Core, IAuthorizationService 권한 부여"
ms.author: riande
manager: wpickett
ms.date: 11/30/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/individual
ms.openlocfilehash: 1864625e0ad6b4ec6fc2ada3fa7d93edec91b633
ms.sourcegitcommit: 037d3900f739dbaa2ba14158e3d7dc81478952ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="articles-based-on-projects-created-with-individual-user-accounts"></a>개별 사용자 계정을 사용 하 여 만든 프로젝트를 기반으로 문서

ASP.NET Core Id는 "개별 사용자 계정" 옵션을 사용 하 여 Visual Studio에서 프로젝트 템플릿을에 포함 됩니다.

인증 템플릿와.NET Core CLI에서 사용할 수 있는 `-au Individual`:

```console
dotnet new mvc -au Individual
dotnet new webapi -au Individual
dotnet new razor -au Individual
```

다음 문서에는 개별 사용자 계정을 사용 하는 ASP.NET Core 서식 파일에서 생성 된 코드를 사용 하는 방법을 보여 줍니다.

* [SMS를 사용한 2단계 인증](xref:security/authentication/2fa)
* [ASP.NET Core의 계정 확인 및 암호 복구](xref:security/authentication/accconfirm)
* [권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기](xref:security/authorization/secure-data)