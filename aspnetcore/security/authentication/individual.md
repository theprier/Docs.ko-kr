---
title: "개별 사용자 계정을 사용 하 여 만든 프로젝트를 기반으로 문서"
author: rick-anderson
description: "이 문서는 개별 사용자 계정을 사용 하 여 만든 프로젝트를 기반으로 문서를 나열 합니다."
ms.author: riande
manager: wpickett
ms.date: 11/30/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/individual
ms.openlocfilehash: 844514f2970b761ec65589765eb21421cd1962a1
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="articles-based-on-projects-created-with-individual-user-accounts"></a><span data-ttu-id="355c7-103">개별 사용자 계정을 사용 하 여 만든 프로젝트를 기반으로 문서</span><span class="sxs-lookup"><span data-stu-id="355c7-103">Articles based on projects created with individual user accounts</span></span>

<span data-ttu-id="355c7-104">ASP.NET Core Id는 "개별 사용자 계정" 옵션을 사용 하 여 Visual Studio에서 프로젝트 템플릿을에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="355c7-104">ASP.NET Core Identity is included in project templates in Visual Studio with the "Individual User Accounts" option.</span></span>

<span data-ttu-id="355c7-105">인증 템플릿와.NET Core CLI에서 사용할 수 있는 `-au Individual`:</span><span class="sxs-lookup"><span data-stu-id="355c7-105">The authentication templates are available in .NET Core CLI with `-au Individual`:</span></span>

```console
dotnet new mvc -au Individual
dotnet new webapi -au Individual
dotnet new razor -au Individual
```

<span data-ttu-id="355c7-106">다음 문서에는 개별 사용자 계정을 사용 하는 ASP.NET Core 서식 파일에서 생성 된 코드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="355c7-106">The following articles show how to use the code generated in ASP.NET Core templates that use individual user accounts:</span></span>

* [<span data-ttu-id="355c7-107">SMS를 사용한 2단계 인증</span><span class="sxs-lookup"><span data-stu-id="355c7-107">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="355c7-108">ASP.NET Core의 계정 확인 및 암호 복구</span><span class="sxs-lookup"><span data-stu-id="355c7-108">Account confirmation and password recovery in ASP.NET Core</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="355c7-109">권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="355c7-109">Create an ASP.NET Core app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
