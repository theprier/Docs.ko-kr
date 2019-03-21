---
ms.openlocfilehash: 6246247788eefc8f094ec1a7f156cb36715edb53
ms.sourcegitcommit: 5f299daa7c8102d56a63b214b9a34cc4bc87bc42
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58210108"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>보안 사용자 데이터 샘플을 빌드/실행 방법

* 암호 관리자 도구를 사용 하 여 암호를 설정 합니다.

  `dotnet user-secrets set SeedUserPW <pw>`

* 데이터베이스를 업데이트 합니다.

  `dotnet ef database update`

* 프로젝트에서 HTTPS를 사용 하도록 설정
