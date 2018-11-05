---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: (Razor) 사이트 페이지는 Asp.net에서 전자 메일 보내기 | Microsoft Docs
author: Rick-Anderson
description: 이 웹 사이트에서 자동화 된 전자 메일 메시지를 전송 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: f388ac1a97bde39cffe6b592b436d7af0d419a5f
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021393"
---
<a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET Web Pages (Razor)를 사용 하는 경우 웹 사이트에서 전자 메일 메시지를 전송 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 웹 사이트에서 전자 메일 메시지를 보내는 방법입니다.
> - 전자 메일 메시지에 파일을 첨부 하는 방법.
> 
> 문서에 도입 된 ASP.NET 기능은 다음과 같습니다.
> 
> - `WebMail` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>웹 사이트에서 전자 메일 메시지 보내기

모든 종류의 웹 사이트에서 전자 메일을 전송 해야 하는 이유가 있습니다. 사용자에 게 확인 메시지를 보낼 수 있습니다 (예를 들어 새 사용자를 등록 합니다.) 자신에 게 알림을 보낼 수 있습니다 또는 `WebMail` 도우미를 사용 하면 쉽게 전자 메일을 보낼 수 있습니다.

사용 하는 `WebMail` 도우미, SMTP 서버에 액세스할 수 있도록 해야 합니다. (SMTP에 대 한 의미 *Simple Mail Transfer Protocol*.) SMTP 서버에만 받는 사람의 서버로 메시지를 전달 하는 전자 메일 서버는 &#8212; 전자 메일의 아웃 바운드 측 것입니다. 웹 사이트에 대 한 호스팅 공급자를 사용 하는 경우는 아마도 설정 전자 메일을 사용 하 여 및 SMTP 서버 이름 이란 알 수 있습니다 수입니다. 회사 네트워크 내에서 작업 하는 경우 관리자 또는 IT 부서 수 일반적으로 정보를 제공 사용할 수 있는 SMTP 서버에 대 한 합니다. 집으로 작업 하는 경우 해당 SMTP 서버의 이름을 알 수 있는 일반 전자 메일 공급자를 사용 하 여 테스트할 수도 있습니다. 일반적으로 필요합니다.

- SMTP 서버의 이름입니다.
- 포트 번호입니다. 이 거의 항상 25입니다. 그러나 ISP 포트 587을 사용 하 여 필요할 수 있습니다. 보안 소켓 레이어 (SSL) 전자 메일을 사용 하는 경우 다른 포트를 해야 할 수 있습니다. 전자 메일 공급자를 사용 하 여 확인 합니다.
- 자격 증명 (사용자 이름, 암호)입니다.

이 절차에서는 두 개의 페이지를 만듭니다. 첫 번째 페이지에 기술 지원 양식에 입력 된 것 처럼 설명을 입력 하는 사용자가 수 있는 양식이 있습니다. 첫 번째 페이지는 두 번째 페이지에 해당 정보를 제출합니다. 두 번째 페이지에서 코드는 사용자의 정보를 추출 하 고 전자 메일 메시지를 보냅니다. 또한 문제 보고서를 받았는지 확인 하는 메시지가 표시 됩니다.

![[이미지]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> 코드를 간단히 유지 하기 위해이 예제에서는 다음을 초기화 합니다.는 `WebMail` 사용할 위치 페이지에서 오른쪽 도우미입니다. 그러나 실제 웹 사이트에 대 한 것을 전역 파일에 다음과 같은 초기화 코드를 저장 하는 것이 좋습니다 초기화할 수 있도록는 `WebMail` 웹 사이트의 모든 파일에 대 한 도우미입니다. 자세한 내용은 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)합니다.


1. 새 웹 사이트를 만듭니다.
2. 명명 된 새 페이지 추가 *EmailRequest.cshtml* 다음 태그를 추가 합니다. 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    다음에 유의 합니다 `action` 폼 요소의 특성으로 설정 되었습니다 *ProcessRequest.cshtml*합니다. 이 폼 현재 페이지로 대신 해당 페이지로 제출할 것을 의미 합니다.
3. 라는 새 페이지 추가 *ProcessRequest.cshtml* 웹 사이트에 다음 코드와 태그를 추가 합니다.   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    코드 페이지에 제출 된 폼 필드의 값을 가져옵니다. 다음 호출을 `WebMail` 도우미의 `Send` 만들고 전자 메일 메시지를 전송 하는 메서드. 이 경우 값을 사용 하 여 폼에서 전송 된 값을 사용 하 여 연결 하는 텍스트의 구성 됩니다.

    이 페이지에 대 한 코드 내에 `try/catch` 블록입니다. 전자 메일 보내기 위해 어떤 이유로 소용이 없으면 (예를 들어 설정을 오른쪽)가 아닌의 코드를 `catch` 블록이 실행 되 고 설정는 `errorMessage` 변수 발생 한 오류를 합니다. (에 대 한 자세한 내용은 `try/catch` 블록 또는 `<text>` 태그를 참조 하십시오 [ASP.NET 웹 페이지 Razor 구문으로 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)

    페이지 본문의 경우는 `errorMessage` 변수가 비어 (기본값), 사용자에 게 전자 메일 메시지가 전송 된 메시지를 표시 합니다. 경우는 `errorMessage` 변수 메시지를 보내는 문제가 되었는지 하는 메시지를 사용자에 게 표시 되는 true로 설정 됩니다.

    오류 메시지가 표시 된 페이지 부분에는 추가 테스트: `if(debuggingFlag)`합니다. 이 전자 메일을 전송 하는 데 문제가 있는 경우 true로 설정할 수 있는 변수입니다. 때 `debuggingFlag` 가 true 이면 추가 오류 메시지를 ASP.NET에서 전자 메일 메시지를 전송 하려고 할 때 보고 항목을 보여 주는 표시는 전자 메일을 보내는 데 문제가 있으면 됩니다. 그러나 상당한 경고,: 전자 메일 메시지를 보낼 수 없는 경우 ASP.NET에서 보고 하는 오류 메시지는 제네릭이 될 수 있습니다. 예를 들어 경우 (예를 들어 있으므로 오류가 서버 이름에 대 한) ASP.NET SMTP 서버에 연결할 수 없습니다, 오류는 `Failure sending mail`합니다.

    > [!NOTE] 
    > 
    > **중요** 예외 개체에서 오류 메시지를 가져올 때 (`ex` 코드에서)를 수행 *하지* 정기적으로 사용자를 통해 해당 메시지를 전달 합니다. 예외 개체에는 사용자가 표시 되지 않습니다 하 고 보안 취약성도 될 수 있는 정보가 종종 포함 됩니다. 때문에 변수를 포함 하는이 코드 `debuggingFlag` 오류 메시지를 표시 하는 스위치와 사용 되는 및 기본적으로 변수가 false로 설정 하는 이유입니다. 변수를 true (및 따라서 오류 메시지 표시)로 설정 해야 *만* 메일을 보내는 중에 문제가 발생 하면 디버깅 해야 할 경우. 문제를 해결 한 후 설정 `debuggingFlag` false 돌아갑니다.

    수정 다음 코드에서 관련 된 설정 전자 메일:

   - 설정 `your-SMTP-host` 에 대 한 액세스를 해야 하는 SMTP 서버의 이름입니다.
   - 설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름입니다.
   - 설정 `your-account-password` SMTP 서버 계정의 암호입니다.
   - 설정 `your-email-address-here` 고유한 전자 메일 주소입니다. 이 메시지에서 전송 되는 전자 메일 주소입니다. (일부 전자 메일 공급자를 사용 하면 다른 지정할 수 없습니다 `From` 해결 하 고 사용자 이름으로 사용 합니다 `From` 주소입니다.)

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>전자 메일 설정 구성
     > 
     > SMTP 서버, 포트 번호 및 등의 올바른 설정을 했는지 확인 하는 경우에 따라 어려울 수 있습니다. 다음은 이에 대한 몇 가지 팁입니다.
     > 
     > - SMTP 서버 이름을 같습니다 종종 `smtp.provider.com` 또는 `smtp.provider.net`합니다. 그러나 사이트를 호스팅 공급자에 게시할 경우 SMTP 서버 이름을 이때 않을 `localhost`합니다. 이것이 게시 한 후 사이트 공급자의 서버에서 실행 되는 전자 메일 서버 응용 프로그램의 관점에서 로컬 수 있기 때문입니다. 서버 이름에서이 변경 내용을 게시 하는 과정의 일부로 SMTP 서버 이름을 변경 해야 될 수도 있습니다.
     > - 포트 번호는 일반적으로 25입니다. 그러나 일부 공급자 포트를 사용 하 여 587 또는 일부 다른 포트가 필요 합니다.
     > - 올바른 자격 증명을 사용 하는지 확인 합니다. 사이트를 호스팅 공급자을 게시 하는 경우 특별히 설정 된 공급자가 전자 메일에 대 한 자격 증명을 사용 합니다. 이러한 게시할 사용 자격 증명과 다를 수 있습니다.
     > - 경우에 따라 전혀 자격 증명이 필요 하지 않습니다. 개인 ISP를 사용 하 여 메일을 보내는 경우 전자 메일 공급자 자격 증명 이미 알고 있습니다. 를 게시 한 후에 로컬 컴퓨터에 테스트 하는 경우 다른 자격 증명을 사용 하는 것이 해야 합니다.
     > - 설정 해야 하는 전자 메일 공급자에서 암호화를 사용 하는 경우 `WebMail.EnableSsl` 에 `true`입니다.
4. 실행 합니다 *EmailRequest.cshtml* 브라우저에서 페이지입니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.)
5. 사용자 이름 및 문제 설명, 입력 한 다음 클릭 합니다 **제출** 단추입니다. 로 리디렉션됩니다 합니다 *ProcessRequest.cshtml* 페이지에서 메시지를 확인 하 고 전자 메일 메시지를 보냅니다는 합니다. 

    ![[이미지]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>전자 메일을 사용 하 여 파일 전송

또한 전자 메일 메시지에 연결 된 파일을 보낼 수 있습니다. 이 절차에서는 텍스트 파일 및 두 개의 HTML 페이지를 만듭니다. 텍스트 파일을 메일 첨부 파일로 사용 합니다.

1. 웹 사이트에서 새 텍스트 파일을 추가 하 고 이름을 *MyFile.txt*합니다.
2. 다음 텍스트를 복사 하 고 파일에 붙여 넣습니다. 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. 라는 페이지를 만듭니다 *SendFile.cshtml* 다음 태그를 추가 합니다. 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. 라는 페이지를 만듭니다 *ProcessFile.cshtml* 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. 수정 다음 전자 메일의 예제에서 코드에서 관련된 설정:

    - 설정 `your-SMTP-host` 에 대 한 액세스를 해야 하는 SMTP 서버의 이름입니다.
    - 설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름입니다.
    - 설정 `your-email-address-here` 고유한 전자 메일 주소입니다. 이 메시지에서 전송 되는 전자 메일 주소입니다.
    - 설정 `your-account-password` SMTP 서버 계정의 암호입니다.
    - 설정 `target-email-address-here` 고유한 전자 메일 주소입니다. (이전에 일반적으로 보내 처럼 전자 메일이 다른 사용자에 게 있지만 테스트용, 있습니다 수 자신에 게 보냅니다.)
6. 실행 합니다 *SendFile.cshtml* 브라우저에서 페이지입니다.
7. 사용자 이름, 제목 줄, 및 연결할 텍스트 파일의 이름을 입력 (*MyFile.txt*).
8. `Submit` 단추를 클릭합니다. 으로 리디렉션됩니다 앞으로 *ProcessFile.cshtml* 페이지에서 메시지를 확인 하 고는 보내는 전자 메일 메시지 첨부 파일을 사용 하 여 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


- [ASP.NET 웹 페이지(Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)
- [Simple Mail Transfer Protocol](https://msdn.microsoft.com/library/aa480435.aspx)
- [ASP.NET 웹 페이지에 대 한 사이트 전체 동작을 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
