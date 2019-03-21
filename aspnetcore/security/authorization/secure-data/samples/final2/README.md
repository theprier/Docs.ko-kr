---
ms.openlocfilehash: 6246247788eefc8f094ec1a7f156cb36715edb53
ms.sourcegitcommit: 5f299daa7c8102d56a63b214b9a34cc4bc87bc42
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58210108"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="4cf00-101">보안 사용자 데이터 샘플을 빌드/실행 방법</span><span class="sxs-lookup"><span data-stu-id="4cf00-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="4cf00-102">암호 관리자 도구를 사용 하 여 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf00-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="4cf00-103">데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf00-103">Update the database:</span></span>

  `dotnet ef database update`

* <span data-ttu-id="4cf00-104">프로젝트에서 HTTPS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4cf00-104">Enable HTTPS in the project</span></span>
