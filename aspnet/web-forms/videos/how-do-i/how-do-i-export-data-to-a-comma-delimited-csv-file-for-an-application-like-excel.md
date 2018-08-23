---
uid: web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
title: '[어떻게 할까요?] Excel 같은 응용 프로그램에 대 한 데이터를 쉼표로 구분 된 (CSV) 파일로 내보내기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서는 Chris Pels 데이터베이스 또는 다른 원본에서 데이터를 가져오고는 응용 프로그램 li에서 사용할 수 있는 쉼표로 구분 된 파일로 내보내야 하는 방법을 표시 하는 중...
ms.author: riande
ms.date: 01/22/2009
ms.assetid: c9df86ad-aec2-43d5-bb8a-413ebb666673
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
msc.type: video
ms.openlocfilehash: 401df30b8f35355ecca5226883bb16b46bf88507
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832098"
---
<a name="how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel"></a><span data-ttu-id="9c9f7-103">[어떻게 할까요?] Excel 같은 응용 프로그램에 대 한 데이터를 쉼표로 구분 된 (CSV) 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="9c9f7-103">[How Do I:] Export Data to a Comma Delimited (CSV) File for an Application Like Excel</span></span>
====================
<span data-ttu-id="9c9f7-104">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="9c9f7-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="9c9f7-105">이 비디오에서는 Chris Pels 데이터베이스 또는 다른 원본에서 데이터를 가져와서 Excel 같은 응용 프로그램에서 사용할 수 있는 쉼표로 구분 된 파일로 내보내야 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c9f7-105">In this video Chris Pels shows how to take data from a database or other source and export it to a comma delimited file that can be used in an application like Excel.</span></span> <span data-ttu-id="9c9f7-106">첫째, 데이터 집합을 DataTable 개체로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9c9f7-106">First, a set of data is created as a DataTable object.</span></span> <span data-ttu-id="9c9f7-107">다음으로, 현재 웹 페이지 요청에 대 한 응답의 선택을 취소 하 고 헤더 및 콘텐츠 형식을 csv 파일로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c9f7-107">Next, the Response for the current web page request is cleared and the header and content type are configured to be a csv file.</span></span> <span data-ttu-id="9c9f7-108">그런 다음 실제 데이터는 첫 번째 데이터 값 뒤에 csv 파일에 대 한 열 헤더를 작성 하 여 응답 스트림에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c9f7-108">Then the actual data is added to the response stream by first writing the column headers for the csv file followed by the data values.</span></span> <span data-ttu-id="9c9f7-109">이 방법은 로컬 Excel과 같은 프로그램에서 조작할 수 있도록 사용자가 데이터의 내보내기를 필요로 하는 경우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c9f7-109">This approach can be useful when users require an export of data so it can be manipulated locally in a program like Excel.</span></span>

[<span data-ttu-id="9c9f7-110">&#9654;비디오 (19 분)</span><span class="sxs-lookup"><span data-stu-id="9c9f7-110">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel)
